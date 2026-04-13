# Swiss MMCE Game Loading — a little PoC I put together

Alright, so I've been tinkering with MMCE game loading in Swiss, and I figured I'd share what came out of it rather than just letting it collect dust on my hard drive. Fair warning up front: this is experimental, very much a proof of concept, and bugs are expected. Please don't file reports — just enjoy it for what it is.

## The honest bit — what doesn't work

- VMC on MMCE is a no-go (it would be pointless anyway)
- Speed isn't great in a bunch of areas, so expect audio stuttering and similar fun
- Only a small selection of games have actually been tested

## The good news

- Games do boot — that part works
- Memory card functionality holds up in most cases

## How this all works under the hood

Swiss patches games to read from alternative sources instead of the DVD drive. The catch is that inside that patch environment, libraries like libOGC2 aren't available — so things like the EXI bus have to be implemented at a much lower level. Fortunately, the Swiss devs (@extrems, @emu_kidid) have done some genuinely impressive groundwork here, and most of what's needed is still usable, just with a different usage pattern than you'd normally reach for.

The MMCE protocol relies on the EXI interrupt pin, and there are two ways to handle that:

- **SW interrupt:** the MMCE device asserts the pin, and the software calls a function in the patch
- **Polling:** the interrupt edge sets a register on the EXI device, which can then be polled in a loop

The first option is obviously the cleaner, faster choice — but I couldn't get it to behave reliably. Sometimes the interrupt simply wouldn't fire in the patch context, leading to the code stalling indefinitely and the game freezing. Not ideal.

So I went with polling, which *does* work to a degree, though it comes with its own baggage:

1. **Idle waiting:** Constantly polling a register for data readiness burns CPU cycles that the game would really rather be using. This leads to game slowdowns — not transfer slowdowns, which is an important distinction.
2. **EXI settle periods:** Even then, polling only became reliable once I added artificial waits between commands. They're small compared to the idle loop overhead, but they're still a bit ugly.

## Download & source

With all that said — I thought this was worth sharing. It shows a concrete path for how MMCE could slot into Swiss's existing game loading architecture, and maybe someone down the line will find a cleaner solution to the interrupt problem.

Sources are [over here](https://github.com/FlipperMCE/swiss-gc/tree/feat/MMCEPatch), and a precompiled version from GitHub Actions is available [here](https://github.com/FlipperMCE/swiss-gc/actions/runs/24345918913/artifacts/6406414012).

Use this with the latest version of *FlipperMCE* firmware.

Even having said all the above: I hope you like it :)

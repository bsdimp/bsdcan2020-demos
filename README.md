# Warner's History of Unix BSDCan 2020 Talk

I did 2 demos in my talk today.

One was for the pdp-7 booting, while the other was for a v6 system.

This repo has images needed to run this, plus instructions for how to build simh and run it.

I've included a couple of other images than what I had in my talk.

## simh

Unfortunately, the pdp-7 in the pkg simh doesn't work. You'll need to build your own:

> git clone https://github.com/philbudne/simh
> cd simh
> make pdp7 pdp11
> sudo cp -p BIN/pdp7 BIN/pdp11 /usr/local/bin

will give you updated binaries. You'll need to build it in special ways to support the graphics card and/or network.

I've also not covered how to put these things on the net. None of the unixes this old supports it.

## PDP-7 Unix

I've included a PDP-7 unix image here. The current tools requires python 2.7 and has some other quirks needed to make them build.

You can find the reconstructed sources in the tuhs archive, or via github at https://github.com/DoctorWkt/pdp7-unix if you want to get the latest.

I didn't build graphics2 support into my simh, so the config script fails to find them.

> cd pdp7-unix
> pdp7 unixv0.simh
>
> PDP-7 simulator V4.0-0 Current        git commit id: d40268d1
> CPU	idle disabled
> 	8KW, EAE
> pdp7/unixv0.simh-13> att rb image.fs
> RB: buffering file in memory
> pdp7/unixv0.simh-18> att -U g2in 12345
> Listening on port 12345
> pdp7/unixv0.simh-25> set g2in disabled
> Command not allowed
> pdp7/unixv0.simh-27> set graphics2 enabled
> Non-existent device
> pdp7/unixv0.simh-28> set graphics2b enabled
> Non-existent device
> pdp7/unixv0.simh-29> set graphics2c enabled
> Non-existent device
> pdp7/unixv0.simh-30> set graphics2d enabled
> Non-existent device
> PDP-7 simulator configuration
>
> CPU	idle disabled
> CLK	60Hz, devno=00
> PTR	devno=01
> PTP	devno=02
> TTI	devno=03
> TTO	devno=04
> LPT	disabled
> DRM	disabled
> RB	devno=71
> DT	disabled
> G2OUT	disabled
> G2IN	disabled
>
> login:

to exit simh, hit ^E. This will get you back to the simh> prompt. You can then quit. If you'd like to login and play around, there's an account 'dmr' with a password of 'dmr'.

## V1 Unix

OK, this isn't a true V1 image. It's a reconstructed unix as it was around
1972. The reconstruction is from two sources. There was a printout of the
slightly post V1 kernel. And there was data recovered from DECtape from around
V2 or V3 (there's ambiguity in the time_t used since it reset the base every
year). You can get the sources from https://github.com/DoctorWkt/unix-jun72 if
you'd like to play.

> % cd v1
> % pdp11 simh.cfg
>
> PDP-11 simulator V3.9-0
> Disabling CR
> Disabling XQ
> RF: buffering file in memory
> simh.cfg> att tc tape
> File open error
> Listening on port 5555 (socket 6)
>
> :login: root
> root
> # ls
> bin
> dev
> etc
> tmp
> # ls -l
> total    5
>  43 sdrwr-  2 root    620 Jan  1 00:00:00 bin
>  42 sdrwr-  2 root    250 Jan  1 00:00:00 dev
> 104 sdrwr-  2 root    110 Jan  1 00:00:00 etc
> 114 sdrwr-  2 root     50 Jan  1 00:00:00 tmp
> # ^E
> Simulation stopped, PC: 007332 (MOV (SP)+,25244)
> sim> quit
> Goodbye
> RF: writing buffer to file
> %

## V5 Unix

This image was pulled from the TUHS archive at https://www.tuhs.org/Archive/Distributions/Research/Dennis_v5/

> cd v5
> pdp11 boot.ini
>
> PDP-11 simulator V3.9-0
> Disabling XQ
> @unix
>
> ;login: root
> # ^E
> Simulation stopped, PC: 001726 (MOV (SP)+,177776)
> sim> quit
> Goodbye

You need to type 'unix' at the @ prompt and then login as root.

V5 only exists as this image. There's no installer.

## V6 Unix

I've included a pre-installed image. You can find the full install instructions at http://gunkies.org/wiki/Installing_Unix_v6_(PDP-11)_on_SIMH which I did for my talk. I've also included the right tapes.

> cd v6
> pdp11 boot.ini
>
> PDP-11 simulator V3.9-0
> Disabling XQ
> LPT: creating new file
> Listening on port 5555 (socket 8)
> @unix
>
> login: root
> # ls
> bin
> dev
> etc
> hpunix
> lib
> mnt
> rkunix
> rpunix
> tmp
> unix
> usr
> # ^E
> Simulation stopped, PC: 002650 (MOV (SP)+,177776)
> sim> quit
> Goodbye

You need to type 'unix' at the @ prompt and then login as root.

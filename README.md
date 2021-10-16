# Demoscenery

Collection of containerized demoscenes.


## About

Demoscene is *realtime* underground digital art.

#### Problems:
 - Video recordings of demoscenes don't match quality of the original — low in resolution and frame rate, lossy audio codecs, fixed aspect ratio; not to mention demoscenes weren't meant to be possible to pause or skip through.
 - Many demoscenes were created decades ago, and require outdated operating systems in order to run.
 - It's generally a bad idea security-wise to execute binaries downloaded from the internet.
#### Solution:
 - Create a collection of demoscene containers using Docker that can be run on any platform and viewed in realtime.


## How it benefits the open-source community

 - Running demoscenes using Wine is a great way to find out what needs to be implmented or fixed in Wine and graphical open-source libraries.


## Known quirks

- Accessing Xpra via http://localhost:10000 prevents sound from being operational, however http://0.0.0.0:10000 seems to work fine.

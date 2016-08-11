# Internet Volume Control.

:warning: this is a work in progress. :warning:

The internet is full of useful information, but with the rise of social media,
there is also a lot of time-wastey Skinnerbox-style sites that keep you coming
back with squirts of dopamine. To help curb this behavior, i've started
developing the Internet Volume Control, which helps give back some control over
how much Noise the internet can deliver.

## Overview

The actual control limiting is done by a custom DNS server, which responds
depending on what the current internet "volume" is. Sites which are very noisy
(e.g. Facebook), are cut off at all but the highest volume levels. Less noisy
sites continue to work, until you dial down the volume. At the lowest volume
level, nothing works.

The Volume Knob - really just a standalone control to manipulate the volume
level. Design still TBD, but could easily be built with a potentiometer and a
little wifi micro, like an esp8266, or a particle photon.

For storing the actual volume level, i'm using http://io.adafruit.com/

### DNS Server

Built around Celluloid::DNS (actually RubyDNS right now..) the server checks a
blacklist of sites to serve NXDomain errors for. If a site is not in the
blacklist for a given volume level, it is passed to upstream servers (google's
Public DNS servers: 8.8.8.8).

#### Future work

 * [ ] Dockerize the server
 * [ ] flag to disable debug/info logs.
 * [ ] token and channel moved to config file, instead of flags.

### Volume Knob

The directory `volumeknob` contiains code for a [Particle](http://particle.io) Photon.
A potentiometer is wired up to pin `A0`, and readings from the pot are converted to volume levels between 0 and 10.
These are then sent to an [AdafriuitIO](http://io.adafruit.com) feed that the DNS Server reads.

#### Future Work

 * [ ] build a fancy enclosure.

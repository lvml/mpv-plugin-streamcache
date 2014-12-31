mpv-plugin-streamcache
======================

mpv plugin for caching live streams robust against network glitches without
lengthening initial cache fill up period.

(written by Lutz Vieweg)

Rationale / Use Case:
=====================

Audio or video live streams (unlike podcasts or other non-live media)
are naturally sent to the client precisely at the bit rate that is
then consumed for replay in the the player software. 

If you start the replay as soon as possible after starting to receive
data, very little data will reside in your player cache, and this amount
will never grow, because all that is received is also replayed right away.

This means that if there are network glitches - think of someone sharing
your InterNet connection exhausting your available downstream bandwidth,
or some intermittent UMTS reception problems - then chances are high you
will experiences unintentional pauses/gaps in the replay.

This is annoying, but usually the only available counter measure is to
not start replaying received data right away, but instead to "wait a
little" for pre-buffering and only then start to play. But this is
annoying, too, because it means you cannot quickly switch/zap between
different live stream programs - think of a dozen shoutcast.com channels
you want to switch between - you really don't want to wait out 10 seconds
of silence or so after switching before you know what's playing.

The streamcache.lua script for mpv provides a solution to this dilemma:
When using it, replay will start right away, but at a slightly reduced
speed (2% slower than normal, by default). This way, more data will be
received than is replayed, so the cache will slowly fill up. Once it is
filled to a reasonable size (by default 30 seconds worth of media, see
the start of the script for configuration options), replay will gradually
accelerate towards 100% / normal speed.

The speed of replay will be adjusted so slowly that you probably 
won't notice it at all.

Of course, this also means it will take considerable time (like 20 minutes
or so) before the maximum desired cache filling is reached, but that's
a fair trade-off: If you listen to a live stream for a long time, you
will very unlikely experience any pauses/gaps, only immediately after
changing channels, you are exposed to the normal risk of network glitches
causing pauses.

Prerequisites / Installation
============================

In order to use streamcache.lua, you only need to have mpv installed.

Usage:
======

mpv --script /path/to/streamcache.lua ...

(Where "..." stands for whatever amount of live stream URLs
you want to put into your playlist. If you don't know what 
kind of URLs to use for testing, visit http://shoutcast.com/
for an index of many web radio stations.

DISCLAIMER
==========

This software is provided as-is, without any warranties.

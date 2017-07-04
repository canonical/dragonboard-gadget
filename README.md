# DragonBoard 410c Gadget Snap

This repository contains the official Ubuntu Core gadget snap for the
DragonBoard 410c.

## Gadget Snaps

Gadget snaps are a special type of snaps that contain device specific support
code and data. You can read more about them in the snapd wiki
https://github.com/snapcore/snapd/wiki/Gadget-snap

## Reporting Issues

Please report all issues on the Launchpad project page
https://bugs.launchpad.net/snap-dragonboard/+filebug

We use Launchpad to track issues as this allows us to coordinate multiple
projects better than what is available with Github issues.

## Building

To build the gadget snap locally please use `snapcraft --target-arch=arm64`.

## Launchpad Mirror and Automatic Builds.

All commits from the master branch of https://github.com/snapcore/dragonboard
are automatically mirrored by Launchpad to the
https://launchpad.net/snap-dragonboard project.

The master branch is automatically built from the launchpad mirror and
published into the snap store to the edge channel.

You can find build history and other controls here:
https://code.launchpad.net/~canonical-foundations/+snap/dragonboard

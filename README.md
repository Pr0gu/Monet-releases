# Monet

Monet is a macOS menu bar app that shows the usage limits of every Claude account you use, all at once.

This repository holds **only Monet's releases**: the notarized disk image of each version, and the signed update
feed (`appcast.xml`) that Monet checks once a day. Monet's source code is private.

## Install

1. Download `Monet-<version>.dmg` from the latest release. Its SHA-256 checksum is next to it:
   `shasum -a 256 -c Monet-<version>.dmg.sha256`.
2. Open it and drag Monet to Applications.
3. Open Monet. macOS asks once whether to open an app downloaded from the internet, and names the developer.
   Monet is notarized by Apple.

After that, Monet updates itself from here. Every update is signed, and Monet checks the signature before it
installs anything.

## Releases

- `v<version>`: Monet. The newest one is marked **Latest**, and its `appcast.xml` is Monet's update feed.
- `dev`: a pre-release test channel that only Monet Dev reads. Monet Dev is the developer's own test build, so
  this channel is not for installing.

Until the first release with a download, the latest release holds only the update feed, and the feed says there
is no update yet.

Monet is an independent app. It is not made by, or affiliated with, Anthropic.

# Overview

pcapper edits pcapng files to remove any information that the user does not
want to share with others. One of its intended purposes is for the submission
of minimal packet captures for bug reporting purposes.

When reporting bugs, large and unwieldy pcapng files are undesirable as they
make it harder to identify the issue. By isolating the bare minimum issue
necessary to reproduce the bug (by removing unrelated information), it speeds
up the debugging process.

Users working on pre-release products can use pcapper to remove as much
identiying information as possible from the capture data.

# Installation

pcapper is intended to use as few Python dependencies as possible and should
"just work".

To install pcapper:

    sudo install -m 755 -o root -g root pcapper /usr/local/bin

# Usage

By default, pcapper will just copy the input to the output:

    pcapper in.pcapng out.pcapng

To use the default anonymization options, provide the `--anon` flag:

    pcapper --anon in.pcapng out.pcapng

To replace MAC addresses and other binary octet sequences, use `--replace`:

    pcapper --replace 11:22:33:44:55:66/00:00:00:00/11:22 in.pcapng out.pcapng

Currently, pcapper replaces any occurrence of the indicated octet sequences. In
the future, pcapper may be extended to intelligently parse the packet data and
only replace octet sequences as appropriate. Currently the intended use of
`--replace` is to sanitize MAC addresses, so the changes of a collission with 6
octets seem low.

# Reference

The excellent [pcapng documentation](https://github.com/pcapng/pcapng) was used
to implement the pcapng parsing.

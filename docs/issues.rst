.. _issues:

Common issues
=============


"Installed rtmpdump does not support ``--jtv`` argument"
--------------------------------------------------------

Your rtmpdump/librtmp is not recent enough. Even though it may
seeem like you have the most recent release (v2.4) it may not be
the correct version. Because of odd release-cycle by the rtmpdump
team, distros may be shipping versions of 2.4 that do not support
the ``--jtv`` parameter.

On Debian/Ubuntu it is recommended to use the official packages
of *librtmp0* and *rtmpdump* version *2.4+20111222.git4e06e21* or newer.

If the correct version of rtmpdump is installed but it's not in your ``$PATH``
you can specify the location with ``--rtmpdump /path/to/rtmpdump``.

If upgrading to a more recent version is not an option, most channels
also have HLS streams available, e.g. *mobile_high*.


"Failed to read data from stream" when trying to play Twitch/Justin.tv streams
------------------------------------------------------------------------------

This may be caused by rtmpdump crashing because of being linked with
a incorrect version of libtmp. Make sure both librtmp and rtmpdump are
the same version.

If you are building rtmpdump yourself it may link with a existing
(probably old) version of librtmp. You can avoid this by building a static
version of rtmpdump, using this make command:

.. code-block:: console

    $ make SHARED=

If this does not help you can get more information by running with ``--errorlog``,
and then look for a log file created in ``/tmp`` that will contain any error messages
from rtmpdump.


Streams are buffering/lagging
-----------------------------

By default most players do not cache the input from stdin, here is a few command
arguments you can pass to some common players:

- ``mplayer --cache <kbytes>`` (between 1024 and 8192 is recommended)
- ``vlc --file-caching <milliseconds>`` (between 1000 and 10000 is recommended)

These options can be used by passing ``--player`` to ``livestreamer``.


Player specific issues
----------------------

VLC fails to play with a error message
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

VLC version *2.0.1* and *2.0.2* contains a bug that prevents it from
reading data from standard input. This has been fixed in version *2.0.3*.

VLC hangs when buffering and no playback starts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Some versions of 64-bit VLC seem to be unable to read the stream created by rtmpdump.
Using the 32-bit version of VLC is a workaround until this bug is fixed.

MPC-HC reports "File not found"
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Reading data from standard input is not supported in the current stable
version of MPC-HC (v1.6.x). However, it was recently added and it looks like
it will be available in 1.7. Nightly builds of 1.7 are available at
http://nightly.mpc-hc.org/.




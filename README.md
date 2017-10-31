# greenctld

A hamlib-compatible driver for the [Green Heron Engineering RT-21 Digital Rotor
Controller](https://www.greenheronengineering.com/prod_documents/controllers/docs/RT-21_Manual_current.pdf).
hamlib does not support the rotor, but this program can be used as a drop-in
replacement for rotctld when commanding the RT-21.

The RT-21 is unlike most of the other rotors hamlib supports in that it uses
two serial ports, one for controlling azimuth and one for controlling
elevation.  The two serial ports are passed via the ```--az-device``` and
```--el-device``` command line arguments.

The TCP network protocol is compatible with the hamlib protocol documented in
the [rotctld(8) man
page](http://manpages.ubuntu.com/manpages/zesty/man8/rotctld.8.html).  This
driver only implements a subset of that protocol, which includes the subset
that [gpredict](http://gpredict.oz9aec.net/) uses.  At [Astro
Digital](https://astrodigital.com/), this driver has been used extensively with
gpredict.  For debugging the network protocol, the ```--dummy``` option can be
used to simulate a rotor without connecting to a real serial port.

Like rotctld, this program does not daemonize on its own.  It also produces
copious debugging output to stdout.

### Usage

 * ```--az-device <serial-port>```, the serial port to use for azimuth

 * ```--el-device <serial-port>```, the serial port to use for elevation

 * ```--speed <baud>```, the serial baud rate to use, defaults to 4800

 * ```--timeout <seconds>```, the serial port timeout, defaults to 1.5

 * ```--port <port>```, the TCP port to listen for connections on, defaults to 4533, the same as rotctld

 * ```--get-pos```, to query the serial ports for the current az/el, and immediately exit.  Useful for testing the serial port configuration.

 * ```--dummy```, to speak the TCP network protocol only without connecting to a serial port, useful for debugging gpredict integration.

### License

Copyright (c) 2017 [Astro Digital, Inc](https://astrodigital.com/)

Released under the terms of the Simplified BSD License; see the [LICENSE](LICENSE) file for details.

### Author

Michael Toren &lt;mct@toren.net&gt;

# eoiptapd

Yet another implementation of MikroTik's EoIP protocol on Linux and TAP devices.

20251230: this is attempt to improve:
sudo make
[ 16%] Building C object CMakeFiles/eoiptapd.dir/eoip.c.o
[ 33%] Building C object CMakeFiles/eoiptapd.dir/socket.c.o
In file included from /usr/include/x86_64-linux-gnu/sys/select.h:30,
                 from /usr/include/x86_64-linux-gnu/sys/types.h:179,
                 from /usr/include/netinet/ip.h:22,
                 from /usr/src/eoiptapd/socket.c:3:
/usr/src/eoiptapd/socket.c: In function ‘socket_listen’:
/usr/src/eoiptapd/socket.c:30:9: error: ‘__arr’ undeclared (first use in this function)
   30 |         FD_ZERO(fd_set);
      |         ^~~~~~~
/usr/src/eoiptapd/socket.c:30:9: note: each undeclared identifier is reported only once for each function it appears in
make[2]: *** [CMakeFiles/eoiptapd.dir/build.make:90: CMakeFiles/eoiptapd.dir/socket.c.o] Error 1
make[1]: *** [CMakeFiles/Makefile2:83: CMakeFiles/eoiptapd.dir/all] Error 2
make: *** [Makefile:91: all] Error 2

## Build

To build this repository, CMake and a compiling toolchain (GCC) are required.

On Linux, simply run following commands:

    cmake .
    make
    
And the executable `eoiptapd` is now ready for you.

## Usage

    eoiptapd -i IF_NAME -l LOCAL_ADDR -r REMOTE_ADDR -t TUNNEL_ID  
    
    LOCAL_ADDR:     local address to bind
    REMOTE_ADDR:    remote address of EoIP tunnel peer
    TUNNEL_ID:      tunnel id
    
## Example

Assumes you have `10.0.0.1` on a MikroTik box, and `10.0.0.2` on a Linux box.

    /interface eoip add local-address=10.0.0.1 remote-address=10.0.0.2 tunnel-id=114
    
    eoiptapd -i tap-eoip -l 10.0.0.2 -r 10.0.0.1 -t 114
    
## License

Source code is published under MIT license. Thanks to @magicnat for the protocol analysis.
 

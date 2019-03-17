# gentoo-distccd-x86

Dockerfile for distccd server on Gentoo based off stage3-x86.

## Startup a Helper node

1. Copy `Dockerfile` to your localhost
2. Build your image via:
   ```
   $ docker build .
   ```
3. Grab your `$imageID`
   ```
   $ docker images
   ```
4. Run your immage and bind it to a TCP/IP port
   ```
   $ docker run -d -p 3632:3632 $imageID
   ```

## Distribute compile to your helper(s)

1. Whitelist your helper(s) IPs in this case `192.168.0.1` on the client side (or whole class C via `192.168.0.0/24`)
   ```
   # /usr/bin/distcc-config --set-hosts "192.168.0.1,cpp,lzo"
   ```
2. Run make or via pump command
   ```
   pump make CC=distcc -j4
   ```
    
## Distributing compiler with Portage

1. Configure your `/etc/portage/make.conf` and run `$ emerge ...` by
  * Set the value of `N` to twice the number of total (local + remote) CPU cores + 1, and
  * Set the value of `M` to the number of local CPU cores
   ```
   # Replace N and M with the right value as calculated previously
   MAKEOPTS="-jN -lM"
   FEATURES="distcc"
   ```
    
Also consult Gentoo's online docs on Distcc.

## References

- [distcc: a fast, free distributed C/C++ compiler](https://github.com/distcc/distcc)
- [Distcc - Gentoo Wiki](http://wiki.gentoo.org/wiki/Distcc)

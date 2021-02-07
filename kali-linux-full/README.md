# kali-linux-everything x86_64

Dockerfile for Kali Linux based off kalilinux/kali-rolling:latest.

## Build and run

1. Copy `Dockerfile` to your localhost
2. Build your image via:
   ```
   $ docker build . -t kali-linux
   ```
3. Run your image and bind it to your graphics etc
   ```
   $ docker run --net="host" --privileged -e DISPLAY=$DISPLAY -it -v /tmp/.X11-unix:/tmp/.X11-unix kali-linux
   ```

## References

- [Kali Linux - Official Tutorials](https://www.kali.org/category/tutorials/)
- [Kali Linux - Penetration Testing Training](https://www.kali.org/penetration-testing-with-kali-linux/)
- [Offensive Security - Kali Training](https://kali.training/)
- [Docker - Getting Started with Docker and basic CLI commands](https://docs.docker.com/get-started/)

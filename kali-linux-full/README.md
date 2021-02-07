# kali-linux-everything x86_64

Dockerfile for Kali Linux based off kalilinux/kali-rolling:latest.

## Build and run

1. Copy `Dockerfile` to your localhost
2. Build your image via:
   ```
   $ docker build . -t kali-linux
   ```
3. Install a VNC client for your localhost
   ```
   $ apt-get install tigervnc
   ```
   Under Gnome you can use `Remote Desktop Viewer`
4. Connect to your `kali-linux` desktop via VNC to `127.0.0.1:5903
   ```
   $ vncviewer 127.0.0.1:5903
   ```
   
### Restarting kali-linux container

Once image is created under the `kali-linux` name, you can restart it (after reboot) or re-attach to it:

1. Start `kali-linux` container
   ```
   $ docker start kali-linux
   ```
2. Reconnect to your desktop via VNC to `127.0.0.1:5903`
2. __Optinal:__ Attach to `kali-linux` console output
   ```
   $ docker attach kali-linux
   ```

## References

- [Kali Linux - Official Tutorials](https://www.kali.org/category/tutorials/)
- [Kali Linux - Penetration Testing Training](https://www.kali.org/penetration-testing-with-kali-linux/)
- [Offensive Security - Kali Training](https://kali.training/)
- [Docker - Getting Started with Docker and basic CLI commands](https://docs.docker.com/get-started/)

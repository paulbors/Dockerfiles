# kali-linux-everything x86_64

Dockerfile for Kali Linux based off kalilinux/kali-rolling:latest.

## Build and run

1. Copy `Dockerfile` to your localhost
2. Build your image via  
   `$ docker build . -t kali-linux`
3. Run `kali-linux` container image  
   `$ docker run --name kali-linux --net="host" --privileged -e DISPLAY=$DISPLAY -it -v /tmp/.X11-unix:/tmp/.X11-unix kali-linux`
4. Inside the container shell, start the VNC server (edit scipt for different settings)  
   `# ./vncstart.sh`
5. Install a VNC client for your localhost  
   `$ apt-get install tigervnc`  
   Under Gnome you can use `Remote Desktop Viewer`.  
   Under Windows you can use `RealVNC`.
6. Connect to your `kali-linux` desktop on DISPLAY :1 via VNC to `127.0.0.1:5903` with `kalitux` as the password  
   `$ vncviewer 127.0.0.1:5903`
   
### Restarting kali-linux container

Once image is created under the `kali-linux` name, you can restart it (after reboot) or re-attach to it:

1. Start `kali-linux` container image  
   `$ docker start kali-linux`
2. Reconnect to your Kali desktop on DISPLAY :1 via VNC to `127.0.0.1:5903` with `kalitux` as the password
2. *Optinal:* Attach to `kali-linux` console output  
   `$ docker attach kali-linux`

## References

- [Kali Linux - Official Tutorials](https://www.kali.org/category/tutorials/)
- [Kali Linux - Penetration Testing Training](https://www.kali.org/penetration-testing-with-kali-linux/)
- [Offensive Security - Kali Training](https://kali.training/)
- [Docker - Getting Started with Docker and basic CLI commands](https://docs.docker.com/get-started/)

# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# From latest rolling release
#  https://hub.docker.com/search?q=kalilinux%2F&type=image
FROM kalilinux/kali-rolling:latest as kali

# Prep container with latest metapackages and install kali-linux-everything
#  https://www.kali.org/news/kali-linux-metapackages/
ENV DEBIAN_FRONTEND noninteractive
RUN \
  apt-get update -y && \
  apt-cache search kali-linux && \
  # Install missing tools
  apt-get install apt-utils && \
  apt-get install pciutils -y && \
  apt-get install iputils-ping -y && \
  apt-get install nano -y && \
  # Install kali-linux-everything packages
  apt-get install kali-linux-everything -y && \
  apt update && \
  # Set the lcale
  echo "LANG=\"en_US.utf8\"" > /etc/locale.gen && \
  locale-gen && \
  # Installing xfce via VNC
  apt-get install kali-desktop-xfce -y && \
  apt-get install tightvncserver -y && \
  apt-get install expect -y
  apt-get install spawn-fcgi -y

# Set the VNC Server password
RUN ( \
    echo "spawn \"/bin/vncpasswd\"" && \
    echo "expect \"Password:\"" && \
    echo "send \"kalitux\r\"" && \
    echo "expect \"Verify:\"" && \
    echo "send \"kalitux\r\"" && \
    echo "expect \"Would you like to enter a view-only password (y/n)?\"" && \
    echo "send \"n\r\"" && \
    echo "expect eof" && \
    echo "exit" && \
    echo "EOF" \
  ) > ./vncpass.exp
RUN expect vncpass.exp

# Run xfce via VNC
ENV USER=root
EXPOSE 5903/tcp
CMD ["tightvncserver", ":1", "-geometry", "1280x800", "-depth", "16", "-pixelformat", "rgb565"]

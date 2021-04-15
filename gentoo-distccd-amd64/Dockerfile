# Copyright 2019 gentoo-distccd-x86 (https://github.com/paulbors/Dockerfiles/blob/master/gentoo-distccd-x86)
#
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

# Name the portage image
FROM gentoo/portage:latest as portage

# Image is based on stage3-amd64
FROM gentoo/stage3-amd64:latest

# Copy the entire portage volume in
COPY --from=portage /var/db/repos/gentoo /var/db/repos/gentoo

# Continue with image build ...
RUN touch /etc/init.d/functions.sh && \
  echo 'PYTHON_TARGETS="${PYTHON_TARGETS} python3_8"' >> /etc/portage/make.conf && \
  echo 'PYTHON_SINGLE_TARGET="python3_8"'             >> /etc/portage/make.conf

# TODO: Set below flags to mirror the hardware for which you're distcc as needed, if needed...
#RUN echo 'CHOST="i686-pc-linux-gnu"'                  >> /etc/portage/make.conf && \
#  echo 'CFLAGS="-O1 -march=atom -mtune=atom -pipe"'   >> /etc/portage/make.conf && \
#  echo 'CXXFLAGS="${CFLAGS}"'                         >> /etc/portage/make.conf

# Sync and install latest gcc and ditstcc
RUN \
  emerge --sync && \
  emerge gcc distcc && \
  rm -rf /var/db/repos/gentoo/*

# Create container startup script
RUN ( \
    echo "#!/bin/sh" && \
    echo "eval \"\`gcc-config -E\`\"" && \
    echo "exec distccd \"\$@\"" \
  ) > /usr/local/sbin/distccd-launcher && \
  chmod +x /usr/local/sbin/distccd-launcher

# Expose distcc port
EXPOSE 3632

# Run startup script and pass distcc its required parameters (allows all connections on 0.0.0.0/0, change as needed)
CMD ["/usr/local/sbin/distccd-launcher", "--allow", "0.0.0.0/0", "--user", "distcc", "--log-level", "notice", "--log-stderr", "--no-detach"]

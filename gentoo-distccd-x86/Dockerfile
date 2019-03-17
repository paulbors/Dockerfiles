# Copyright 2019 Paul C Bors
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

# Image is based on stage3-x86
FROM gentoo/stage3-x86:latest

# Copy the entire portage volume in
COPY --from=portage /usr/portage /usr/portage

# Continue with image build ...
RUN touch /etc/init.d/functions.sh && \
  echo 'PYTHON_TARGETS="${PYTHON_TARGETS} python2_7"' >> /etc/portage/make.conf && \
  echo 'PYTHON_SINGLE_TARGET="python2_7"' >> /etc/portage/make.conf

RUN \
  emerge --sync && \
  emerge gcc distcc
  rm -rf /usr/portage/*

RUN ( \
    echo "#!/bin/sh" && \
    echo "eval \"\`gcc-config -E\`\"" && \
    echo "exec distccd \"\$@\"" \
  ) > /usr/local/sbin/distccd-launcher && \
  chmod +x /usr/local/sbin/distccd-launcher

EXPOSE 3632

CMD ["/usr/local/sbin/distccd-launcher", "--allow", "0.0.0.0/0", "--user", "distcc", "--log-level", "notice", "--log-stderr", "--no-detach"]

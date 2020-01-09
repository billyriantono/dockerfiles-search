FROM fedora:29

RUN dnf install -y git \
  bzip2 \
  scons \
  protobuf-compiler \
  python2-protobuf

RUN set -o pipefail && \
  curl https://armkeil.blob.core.windows.net/developer/Files/downloads/gnu-rm/8-2018q4/gcc-arm-none-eabi-8-2018-q4-major-linux.tar.bz2 | tar -C /opt -xjf - && \
  echo "export PATH=/opt/gcc-arm-none-eabi-8-2018-q4-major/bin:$PATH" > /etc/profile.d/arm-none-eabi_path.sh

FROM bdero/devkitarm-3ds
MAINTAINER Brandon DeRosier "x@bdero.me"

RUN apt-get update && \
  apt-get install -y python3 && \
  rm -rf /var/lib/apt/lists/* && \
  ln -s /usr/bin/python3 /usr/bin/python

WORKDIR /opt/devkitPro
RUN git clone --depth=1 https://github.com/smealum/aemstro.git && \
  git clone --depth=1 https://github.com/xerpi/sf2dlib.git

WORKDIR /opt/devkitPro/sf2dlib/libsf2d
ENV AEMSTRO /opt/devkitPro/aemstro
RUN make && \
  make install
WORKDIR /source
CMD ["bash"]


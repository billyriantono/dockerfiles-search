FROM fsharp:4
LABEL \
  version="1.0" \
  description="Liquid Quantum Simulator" \
  howto="https://blogs.msdn.microsoft.com/uk_faculty_connection/2017/10/11/getting-started-with-liqui-and-quantum-computing/" \
  maintainer="abautu@gmail.com"
RUN \
  apt-get update &&\
  DEBIAN_FRONTEND=noninteractive apt-get -y install wget bsdtar &&\
  rm --recursive --force /var/lib/apt/lists/* &&\
  cd / &&\
  wget --quiet --output-document=- https://github.com/StationQ/Liquid/archive/master.zip | bsdtar -xf- &&\
  mv Liquid-master Liquid &&\
  echo 'alias Liquid="mono /Liquid/linux/Liquid.exe"' >> /root/.bashrc &&\
  mkdir -p /work
COPY ./docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
VOLUME /work
WORKDIR /work

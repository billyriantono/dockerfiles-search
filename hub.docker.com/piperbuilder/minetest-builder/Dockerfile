FROM piperbuilder/ubuntu-builder
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y make cmake gcc-arm-linux-gnueabihf g++-arm-linux-gnueabihf pkg-config-arm-linux-gnueabihf
WORKDIR /home/piper
ARG REPO_USER
ENV REPO_USER $REPO_USER
COPY . piper-builder-minetest
WORKDIR piper-builder-minetest
RUN ./unpack-erootfs.sh
RUN tar -xzf archive/erootfs-libs-stripped.tar.gz
RUN ./build.sh irrlicht
RUN ./build.sh minetest
CMD ./build.sh

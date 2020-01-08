FROM ubuntu:18.04

RUN apt-get update && apt-get install -y build-essential libsdl2-dev libopenal-dev libgtk-3-dev libpng-dev zlib1g-dev libwebkitgtk-3.0-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libjpeg-dev libssl-dev libvorbis-dev libogg-dev uuid-dev

WORKDIR /main/platform/linux
ENTRYPOINT [ "/main/platform/linux/build_template_linux.sh" ]

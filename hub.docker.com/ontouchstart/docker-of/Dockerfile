FROM debian:8
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install -y curl wget vim
RUN curl -O http://openframeworks.cc/versions/v0.9.8/of_v0.9.8_linux64_release.tar.gz 
RUN tar -xzvf of_v0.9.8_linux64_release.tar.gz
COPY ./install_dependencies.sh /of_v0.9.8_linux64_release/scripts/linux/debian/install_dependencies.sh
COPY ./install_codecs.sh /of_v0.9.8_linux64_release/scripts/linux/debian/install_codecs.sh
RUN /of_v0.9.8_linux64_release/scripts/linux/debian/install_dependencies.sh
RUN /of_v0.9.8_linux64_release/scripts/linux/debian/install_codecs.sh
RUN /of_v0.9.8_linux64_release/scripts/linux/compileOF.sh -j3
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y build-essential nodejs cmake python2.7 git
RUN curl -O https://s3.amazonaws.com/mozilla-games/emscripten/releases/emsdk-portable.tar.gz
RUN tar -xzvf emsdk-portable.tar.gz
RUN cd /emsdk-portable && ./emsdk update && ./emsdk install latest && ./emsdk activate latest

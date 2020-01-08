FROM ubuntu:16.04
RUN sed -i -- 's/#deb-src/deb-src/g' /etc/apt/sources.list
RUN apt-get update && apt-get install -y qt5-default libxcb-xinerama0-dev build-essential perl python git
COPY .git qtbase/.git
RUN cd qtbase/ \
 && git reset --hard HEAD \
 && ./configure -developer-build -confirm-license -opensource -nomake examples -nomake tests

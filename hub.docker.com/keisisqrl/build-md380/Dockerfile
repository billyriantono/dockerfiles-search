FROM ubuntu:latest
RUN apt-get update && apt-get install -y build-essential zip unzip curl \
    gcc-arm-none-eabi libnewlib-arm-none-eabi python git python-usb
RUN mkdir /workdir
WORKDIR /workdir
ENTRYPOINT ["/usr/bin/make"]
CMD ["distclean", "dist"]

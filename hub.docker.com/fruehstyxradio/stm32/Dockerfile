FROM ubuntu:bionic
RUN apt-get update && apt-get install -y software-properties-common build-essential apt-utils
RUN apt-get install -y git flex bison cmake doxygen gcc-arm-none-eabi screenfetch
ENTRYPOINT screenfetch

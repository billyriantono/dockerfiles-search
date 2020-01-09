FROM balenalib/raspberrypi3
ENV DEBIAN_FRONTEND noninteractive
RUN [ "cross-build-start" ]

RUN apt-get update && apt-get install -y binutils wget zip unzip xz-utils

WORKDIR /home/piper

ENV RASPBIAN_LATEST raspbian-2018-06-29/2018-06-27-raspbian-stretch.zip
RUN wget -q -O raspbian_latest https://downloads.raspberrypi.org/raspbian/images/$RASPBIAN_LATEST

COPY --from=piperbuilder/pipercode /usr/local/lib/nodejs/ nodejs/
COPY . ./

RUN [ "cross-build-end" ]

VOLUME /mnt/scratch
CMD [ "./build.sh" ]

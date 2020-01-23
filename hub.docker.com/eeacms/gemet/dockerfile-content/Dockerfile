FROM debian:9.8-slim AS Base

ENV FFMPEG_VERSION=3.0.2

WORKDIR /tmp/ffmpeg

RUN apt-get update 
RUN apt-get install -y ffmpeg
RUN apt-get install -y wget

FROM Base as AzCopyBase

WORKDIR /tmp/azcopyinstall

RUN wget -O azcopyv10.tar https://aka.ms/downloadazcopy-v10-linux
RUN tar -xf azcopyv10.tar
RUN mv azcopy_linux_amd64_10.0.8/azcopy /azcopy
RUN rm -r /tmp

FROM AzCopyBase
WORKDIR /
COPY ./clip_and_upload.sh /
COPY ./clip_and_upload_with_args.sh /
COPY ./waiting_loop.sh /
RUN chmod +x /waiting_loop.sh
RUN chmod +x /clip_and_upload.sh
RUN chmod +x /clip_and_upload_with_args.sh
RUN apt-get clean

# ENTRYPOINT ["/clip_and_upload.sh"]

#CMD []

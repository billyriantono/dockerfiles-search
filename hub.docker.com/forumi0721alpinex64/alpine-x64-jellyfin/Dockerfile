ARG BUILD_ARCH=x64

FROM forumi0721alpine${BUILD_ARCH}build/alpine-${BUILD_ARCH}-ffmpeg-build:latest as ffmpeg

#FROM forumi0721alpine${BUILD_ARCH}build/alpine-${BUILD_ARCH}-skiasharp-build:latest as skiasharp

FROM forumi0721alpine${BUILD_ARCH}/alpine-${BUILD_ARCH}-dotnet-2-sdk:latest as builder

LABEL maintainer="forumi0721@gmail.com"

ENV DOTNET_RUNTIME=linux-musl-x64

COPY build/. /usr/local/

#RUN ["docker-build-start"]

RUN ["docker-init"]

#RUN ["docker-build-end"]

COPY --from=ffmpeg /opt/ffmpeg /opt/ffmpeg

#COPY --from=skiasharp /opt/skia/libSkiaSharp.so /opt/jellyfin/



FROM forumi0721/alpine-x64-base:latest

LABEL maintainer="forumi0721@gmail.com"

COPY --from=builder /opt /opt

COPY local/. /usr/local/

#RUN ["docker-build-start"]

RUN ["docker-init"]

#RUN ["docker-build-end"]

ENTRYPOINT ["docker-run"]

EXPOSE 8096/tcp 8920/tcp

VOLUME /conf.d


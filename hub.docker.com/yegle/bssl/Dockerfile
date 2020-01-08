FROM debian:stable as build_env

RUN apt-get update
RUN apt-get install -y git cmake build-essential golang

RUN git clone https://boringssl.googlesource.com/boringssl

RUN mkdir build
WORKDIR build
RUN cmake ../boringssl
RUN make
RUN strip tool/bssl

FROM gcr.io/distroless/cc

COPY --from=build_env /build/tool/bssl /bin/bssl

ENTRYPOINT ["/bin/bssl"]

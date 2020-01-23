FROM alpine:3.10 AS builder

RUN apk add --no-progress --no-cache \
    cmake=3.14.5-r0 \
    yasm=1.3.0-r1 \
    ninja=1.9.0-r1 \
    gcc=8.3.0-r0 \
    g++=8.3.0-r0

WORKDIR /build
COPY Source Source/
COPY third_party third_party/
COPY CMakeLists.txt CMakeLists.txt

WORKDIR /build/Release
RUN cmake .. -G"Ninja" -DBUILD_DEC=OFF -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=OFF && ninja

FROM alpine:3.10
LABEL maintainer="Christopher Degawa <ccom@randomderp.com>" \
    name="SVT-AV1" \
    description="SVT-AV1 encoder" \
    vcs-url="https://github.com/OpenVisualCloud/SVT-AV1" \
    License="BSD-2-Clause-Patent" \
    version="0.0.1"
COPY --from=builder /build/Bin/Release/SvtAv1EncApp /
ENTRYPOINT [ "/SvtAv1EncApp" ]
CMD [ "-help" ]
# Example: ffmpeg -i Bin/akiyo_cif.y4m -nostdin -f rawvideo -pix_fmt yuv420p - | docker run -i 1480c1/svt-av1 -i stdin -n 300 -w 352 -h 288 -b test.ivf && docker cp $(docker ps -al --format "{{.Names}}"):test.ivf .
# docker run -i 1480c1/svt-av1 -i stdin -n 300 -w 352 -h 288 -b test.ivf < akiyo_cif.y4m  && docker cp $(docker ps -al --format "{{.Names}}"):test.ivf .

FROM alpine:3.8 AS musl
RUN [ "apk", "add", "--no-cache", "llvm5" ]
RUN [ "apk", "add", "--no-cache", "clang" ]
RUN [ "apk", "add", "--no-cache", "make" ]
ENV CC=clang CROSS_COMPILE=llvm-

WORKDIR /src
COPY musl .
RUN [ \
	"./configure", \
	"--prefix=/pkg", "--disable-wrapper", \
	"--enable-debug", "--disable-shared", \
	"--enable-warnings" \
]
RUN [ "make", "-j4" ]
RUN [ "make", "install" ]

FROM scratch
COPY --from=musl /pkg /

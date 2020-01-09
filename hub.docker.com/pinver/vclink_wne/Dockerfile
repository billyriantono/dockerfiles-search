FROM alpine:3.4

RUN apk --no-cache add wine freetype ncurses file
ENV WINEARCH=win64
RUN wineboot init

ENV WINEDEBUG=-all

ADD vc /vc
ENV WINEDLLOVERRIDES="MSVCP140,vcruntime140,ucrtbase,api-ms-win-crt-locale-l1-1-0,api-ms-win-crt-runtime-l1-1-0,api-ms-win-crt-stdio-l1-1-0,api-ms-win-crt-heap-l1-1-0,api-ms-win-crt-conio-l1-1-0=n"

CMD ["wine64", "vc/bin/link.exe"]

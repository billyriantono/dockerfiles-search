FROM  arm32v6/alpine:3.9 as builder

COPY ./qemu-arm-static /usr/bin/qemu-arm-static

RUN apk add --update upx python python-dev  py-pip \
  && apk add build-base libffi-dev openssl-dev zlib-dev\
  && pip install pyinstaller python-telegram-bot transmission-clutch

COPY ./filebot.py /app/
WORKDIR /app
 
RUN pyinstaller --onefile filebot.py 
RUN chmod +x /app/dist/filebot

FROM arm32v6/alpine:3.9

COPY ./qemu-arm-static /usr/bin/qemu-arm-static
COPY --from=builder /app/dist/filebot /filebot

CMD ["/filebot"]

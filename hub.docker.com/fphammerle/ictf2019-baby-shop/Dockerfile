FROM debian:buster-slim

COPY ./ld-2.28.so /home/baby_shop/
COPY ./libc.so.6 /
COPY ./baby_shop /

ENV LD_PRELOAD=/libc.so.6
CMD ["/baby_shop"]

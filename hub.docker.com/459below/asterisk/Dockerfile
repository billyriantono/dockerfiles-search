FROM debian

RUN apt update && apt install -y \
 asterisk \
 asterisk-opus \
 asterisk-core-sounds-en-g722 \
 asterisk-moh-opsound-g722 \
 mpg123 \
 && rm -rf /var/lib/apt/lists/*

EXPOSE 5060/udp
EXPOSE 5061/tcp
EXPOSE 4569/tcp
EXPOSE 4569/udp
EXPOSE 10000-10010/udp
EXPOSE 2727/udp

CMD ["asterisk", "-g", "-f", "-U", "asterisk"]

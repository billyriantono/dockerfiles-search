FROM alpine:3.8

RUN apk add --no-cache tftp-hpa
VOLUME /tftpboot
EXPOSE 69/udp
ENTRYPOINT ["in.tftpd"]
CMD ["-c", "-L", "--secure", "/tftpboot"]

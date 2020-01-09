# Docker-alpine-tftp
FROM alpine:3.6

MAINTAINER Sean Mollet sean@malmoset.com

# Start the container with the follonwing command:
#   docker run -it -p 69:69 -v $(pwd):/tftpboot --name tftp smollet/tftp

#Create user
RUN adduser -S tftp

#Install tftp
RUN apk update
RUN apk add tftp-hpa busybox

#Create the volume for served files
VOLUME /tftpboot

EXPOSE 69

CMD ["sh", "-c", "busybox syslogd -n -O /dev/stdout & in.tftpd -Lvv --user tftp --address 0.0.0.0:69  --secure /tftpboot"]

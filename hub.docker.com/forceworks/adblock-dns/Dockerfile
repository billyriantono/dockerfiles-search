### if you want to build the image run the following command ($pwd has to be this directory)
### docker build . --force-rm -t forceworks/adblock-dns
### if you want to run your locally built container use the command below
### docker run -d -p 53:53/tcp -p 53:53/udp --dns 8.8.8.8 --name adblock-dns forceworks/adblock-dns

FROM alpine
LABEL maintainer="forceworks@forceworks.nl"
COPY buildscript.sh /root/
COPY entrypoint.sh /
COPY *.hosts /root/
RUN apk --no-cache add dnsmasq curl && sh /root/buildscript.sh
COPY dnsmasq.conf /etc/dnsmasq.conf
EXPOSE 53 53/udp
EXPOSE 53 53/tcp
ENTRYPOINT [ "sh", "entrypoint.sh" ]
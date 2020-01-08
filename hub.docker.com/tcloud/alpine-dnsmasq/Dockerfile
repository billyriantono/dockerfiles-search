FROM tcloud/alpine-base

RUN apk --no-cache add dnsmasq

EXPOSE 53 53/udp

VOLUME ["/data","/log"]
    
CMD ["dnsmasq", "-k"]
from alpine 
label mantainer <renanqts@gmail.com>

# install bind
RUN apk --update add bind bash

# standard config
COPY named.conf /etc/bind/

EXPOSE 53
EXPOSE 53/udp

CMD ["named", "-c", "/etc/bind/named.conf", "-g", "-u", "named"]

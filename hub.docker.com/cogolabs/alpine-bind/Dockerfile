FROM alpine
RUN apk update && apk add bind
ADD named.conf /etc/bind/named.conf
CMD ["named", "-4", "-g"]

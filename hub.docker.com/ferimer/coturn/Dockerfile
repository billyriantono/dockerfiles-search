FROM alpine:latest
MAINTAINER Ferimer DevTeam <devteam@ferimer.es>

RUN apk add coturn openssl

ENV TURN_PORT 3478
ENV TURN_PORT_START 10000
ENV TURN_PORT_END 20000
ENV TURN_SECRET mysecret
ENV TURN_SERVER_NAME coturn
ENV TURN_REALM mydomain.tld

ADD start_coturn.sh start_coturn.sh
ADD generate_user.sh generate_user.sh

EXPOSE 3478
EXPOSE 10000-20000

CMD ["/start_coturn.sh"]

FROM debian:stable

CMD [ "/bin/bash" ]

RUN apt-get update \
 && apt-get dist-upgrade -y \
 && apt-get install -y bash curl openssh-client net-tools dnsutils postgresql-client jq

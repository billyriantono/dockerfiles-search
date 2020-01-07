FROM debian:stretch

ENV APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn \
    DEBIAN_FRONTEND=noninteractive
    
RUN apt-get update && apt-get -yq install curl jq

ADD run.sh /run.sh

CMD [ "/bin/bash", "/run.sh" ]
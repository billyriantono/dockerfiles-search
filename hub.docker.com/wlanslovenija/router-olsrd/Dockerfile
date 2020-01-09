FROM tozd/runit

RUN apt-get update -q -q && apt-get install olsrd olsrd-plugins iproute2 --yes --force-yes

COPY ./etc /etc


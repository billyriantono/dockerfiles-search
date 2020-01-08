FROM osrm/osrm-backend:v5.21.0

RUN apt-get -y update

RUN apt-get -y install \
    awscli \
    curl \
    osmium-tool

WORKDIR /apps/

COPY bootstrap.sh bootstrap.sh
RUN chmod +x bootstrap.sh

CMD ["./bootstrap.sh", "-dwt"]

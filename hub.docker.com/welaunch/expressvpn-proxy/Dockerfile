FROM debian:10.1

ENV ACTIVATION_CODE code
ENV SERVER smart

ARG APP=expressvpn_2.2.0-1_amd64.deb

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates wget expect iproute2 net-tools vim dante-server \
    && wget -q "https://download.expressvpn.xyz/clients/linux/${APP}" -O /tmp/${APP} \
    && dpkg -i /tmp/${APP}

WORKDIR /src

COPY entrypoint.sh entrypoint.sh
COPY activate.sh activate.sh

COPY danted.conf /etc/danted.conf

EXPOSE 1080

ENTRYPOINT ["/bin/bash", "entrypoint.sh"]
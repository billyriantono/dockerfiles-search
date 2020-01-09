FROM        debian:stable-slim

ENV         DEBIAN_FRONTEND noninteractive

RUN      apt update -y \
            && apt install -y libatomic1 libstdc++6 curl gnupg dirmngr iproute2 \
            && useradd -d /home/container -m container

RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg \
    && mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/ \
    && curl -o /etc/apt/sources.list.d/microsoft-prod.list https://packages.microsoft.com/config/debian/10/prod.list \
    && apt update \
    && apt install aspnetcore-runtime-3.0 -y

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh
CMD ["/bin/bash", "/entrypoint.sh"]

FROM            ubuntu:latest

## System upgrade
RUN ( \
        apt-get update && \
        apt-get --yes --assume-yes install smartmontools \
    )

ENTRYPOINT ["smartctl"]


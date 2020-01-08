# based on Linux Alpine, used for building RocksDB
FROM ubuntu:18.04
ARG DEBIAN_FRONTEND=noninteractive

ENV BRANCH_SELECTED=master
ENV HOSTNAME=localhost
ENV STRATUM_PORT=40403
ENV STATUS_PORT=8001
ENV PEER_ID=/opt/peer_id.json

RUN export LC_ALL=en_US.utf-8 && export LANG=en_US.utf-8

RUN apt-get update 

RUN apt-get install -y python3-pip git python3-structlog && python3 -m pip install --user pipenv && export PATH="${HOME}/.local/bin:$PATH"

RUN git clone https://github.com/hathornetwork/hathor-core.git

WORKDIR hathor-core/

RUN git checkout ${BRANCH_SELECTED} 

RUN export PATH="${HOME}/.local/bin:$PATH"

RUN export LC_ALL=C.UTF-8 && export LANG=C.UTF-8 && python3 -m pipenv sync -d --bare
RUN export LC_ALL=C.UTF-8 && export LANG=C.UTF-8 && python3 -m pipenv shell --fancy && python3 -m pipenv run make protos

EXPOSE 40403 8080 8001

COPY entrypoint.sh ./entrypoint.sh

ENTRYPOINT [ "bash", "entrypoint.sh"]
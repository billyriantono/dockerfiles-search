# Run sceptre in a container
# docker run --rm -it -v $HOME/.aws:/root/.aws:ro -v $(pwd):/workdir:ro craighurley/docker-sceptre

FROM        python:3.6-alpine3.9
MAINTAINER  Craig Hurley

WORKDIR     /workdir

COPY        docker-entrypoint.sh /usr/local/bin/

RUN         chmod +x /usr/local/bin/docker-entrypoint.sh \
            && pip3 install --no-cache-dir \
                requests \
                sceptre==1.4.2

ENTRYPOINT  [ "docker-entrypoint.sh" ]

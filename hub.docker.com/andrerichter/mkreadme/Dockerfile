FROM ubuntu:16.04
MAINTAINER Andre Richter <andre.o.richter@gmail.com>

RUN apt-get update -q &&                       \
    apt-get install -y --no-install-recommends \
    pandoc

RUN apt-get update -q -y  &&                      \
    apt-get install -q -y --no-install-recommends \
        pandoc &&                                 \
    apt-get autoremove -q -y &&                   \
    apt-get clean -q -y &&                        \
    rm -rf /var/lib/apt/lists/*

RUN apt-get clean autoclean

COPY github-pandoc.css /src/
COPY render.sh /src/

VOLUME ["/work"]
WORKDIR /work

ENTRYPOINT ["bash", "/src/render.sh"]
CMD ["README.md"]

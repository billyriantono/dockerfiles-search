FROM sharelatex/sharelatex

RUN apt-get update && apt-get install -y \
    texlive-full

EXPOSE 80

WORKDIR /

ENTRYPOINT ["/sbin/my_init"]

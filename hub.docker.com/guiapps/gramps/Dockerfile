FROM debian

LABEL maintainer "Sergei O. Udalov <sergei.udalov@gmail.com>"

RUN apt-get update \
    && apt-get install -y gramps \
    && rm -rf /var/lib/apt/lists/*

CMD ["gramps"]

FROM debian:stretch-slim

RUN apt-get update \
 && apt-get install -y --no-install-recommends mupdf \
 && rm -fr /var/lib/apt/lists/*

CMD ["mupdf"]

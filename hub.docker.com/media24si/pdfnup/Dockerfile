FROM ubuntu:18.04
RUN apt update && apt install -y texlive-extra-utils && rm -rf /var/lib/apt/lists/*
WORKDIR /work
ENTRYPOINT ["/usr/bin/pdfnup"]
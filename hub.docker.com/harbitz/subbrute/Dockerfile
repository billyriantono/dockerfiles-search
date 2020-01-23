FROM debian:bullseye-slim
RUN mkdir output
COPY run.sh .
RUN apt-get update && apt-get install -y \
    git \
    python3-pip \
 && rm -rf /var/lib/apt/lists/*
RUN git clone https://github.com/TheRook/subbrute
WORKDIR /subbrute
ENTRYPOINT ["/run.sh"]
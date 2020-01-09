FROM debian:bullseye-slim
RUN mkdir output
COPY run.sh .
RUN apt-get update && apt-get install -y \
    git \
    python3-pip \
 && rm -rf /var/lib/apt/lists/*
RUN git clone https://github.com/chris408/ct-exposer
RUN pip3 install -r /ct-exposer/requirements.txt
ENTRYPOINT ["/run.sh"]
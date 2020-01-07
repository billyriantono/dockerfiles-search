FROM ubuntu:latest

RUN apt-get update && apt-get install -y \
    wget \
    libgmp10 \
&& rm -rf /var/lib/apt/lists/*

RUN wget https://launchpad.net/~kflarsen/+archive/ubuntu/mosml/+files/mosml_2.10.1-0ubuntu0_amd64.deb
RUN dpkg -i mosml_2.10.1-0ubuntu0_amd64.deb
RUN rm mosml_2.10.1-0ubuntu0_amd64.deb

CMD ["mosml", "-P", "full"]

FROM ubuntu:16.04

RUN apt update -y

RUN apt install -y curl \
	ca-certificates 

RUN useradd -ms /bin/bash nodeuser

USER nodeuser
WORKDIR /home/nodeuser

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash

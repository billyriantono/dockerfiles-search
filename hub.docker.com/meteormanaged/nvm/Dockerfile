FROM debian:jessie-slim

RUN apt-get update && apt-get -y install curl

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash 

RUN . ~/.bashrc \
	&& nvm install node \
	&& nvm version

RUN mkdir -p /usr/src/workdir

WORKDIR /usr/src/workdir

RUN /bin/bash --login -c "node -v"

CMD ["/bin/bash --login -c 'npm start'"]
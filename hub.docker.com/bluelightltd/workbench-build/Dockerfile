FROM bluelightltd/workbench-fullbase

RUN apt-get -y remove docker docker-engine && curl -fsSL https://get.docker.com -o get-docker.sh \
	&& sh get-docker.sh \
	&& curl -L https://github.com/docker/compose/releases/download/1.23.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose \
    	&& chmod +x /usr/local/bin/docker-compose \
	&& which docker && docker -v && which dockerd && dockerd -v && which docker-compose && docker-compose version 

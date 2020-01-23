FROM ubuntu
MAINTAINER Cristian Dinu @cdinu

RUN apt-get update
RUN apt-get install -y curl wget
RUN curl --silent --location https://deb.nodesource.com/setup_0.12 | sudo bash -
RUN apt-get install -y zsh vim mc git nodejs tmux
RUN wget -qO- https://get.docker.com/ | sh
RUN npm i -g jshint jscs webpack webpack-dev-server

COPY .* * /dot-files/
RUN cd /dot-files && ./install.sh


# run your container with
# docker run --name golem --hostname golem -ti -v $PWD:/host/current -v $HOME:/host/home -v /var/run:/var/run -v $HOME/.ssh:/root/.ssh:ro --privileged  cdinu/dev-machine /bin/zsh

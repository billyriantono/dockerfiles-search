FROM selenium/node-chrome

USER root

RUN apt-get update -yq && apt-get upgrade -yq && \
apt-get -y -f install \ 
	wget \ 
	unzip \
	nodejs \
	npm
RUN npm cache clean -f && npm install -g n && n stable

COPY assignment.sh /assignment.sh

RUN chmod a+x /assignment.sh

# Container entry point
ENTRYPOINT ["/assignment.sh"]







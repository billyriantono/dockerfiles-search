FROM node

# Declare maintainer
MAINTAINER stephanelaverdure <stephanelaverdure@hotmail.fr>

RUN npm install ungit -g

EXPOSE 8448

ENV HOME /home/developer
RUN useradd --create-home --home-dir $HOME developer \
	&& chown -R developer:developer $HOME

WORKDIR /home/developer
USER developer

CMD ["/usr/local/bin/ungit", "--no-launchBrowser", "--forcedLaunchPath=$HOME"]

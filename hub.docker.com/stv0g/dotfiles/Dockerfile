FROM debian

MAINTAINER "Steffen Vogel <post@steffenvogel.de>"

# Update packages
RUN sed -i 's|http://httpredir.debian.org|ftp://ftp.halifax.rwth-aachen.de|g' /etc/apt/sources.list
RUN apt-get update -y && apt-get install -y curl git

# Install dotfiles
WORKDIR /root
RUN curl -sSL https://raw.githubusercontent.com/stv0g/dotfiles/master/bootstrap.sh | bash

CMD /bin/bash

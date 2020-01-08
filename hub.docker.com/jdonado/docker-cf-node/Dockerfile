FROM node:8.9.4
MAINTAINER F. Javier R. Donado <javier.donado@porsche.digital>

# Install CloudFoundry CLI
RUN cd ~
ADD https://cli.run.pivotal.io/stable?release=debian64&source=github /tmp/cf-installer.deb
RUN dpkg -i /tmp/cf-installer.deb && apt-get install -f



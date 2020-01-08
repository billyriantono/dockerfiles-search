FROM sporsh/nvm
MAINTAINER  Geir Sporsheim <geir.sporsheim@gmail.com>


# Install Node.js
RUN echo 'nvm install 0.11' | bash -l
RUN echo 'nvm alias default 0.11' | bash -l


# Git is required for installing some bower components
USER root
RUN apt-get -y install git
USER nvm

# Install bower
RUN echo 'npm install -g bower' | bash -l


# Install grunt
RUN echo 'npm install -g grunt-cli' | bash -l

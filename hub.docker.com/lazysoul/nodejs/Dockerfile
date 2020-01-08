FROM lazysoul/ubuntu:latest

# Install NodeJS V12
RUN apt-get update
RUN apt-get -y install dialog apt-utils
RUN apt-get -y install dirmngr apt-transport-https lsb-release ca-certificates
RUN curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
RUN apt-get -y install nodejs gcc g++ make

# NVM
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
RUN echo 'export NVM_DIR="$HOME/.nvm"'
RUN echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"'
RUN echo '[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"'

RUN source  ~/.nvm/nvm.sh && nvm install --lts

RUN npm install -g http-server

# Add additional tools
RUN apt-get install -y links git htop

CMD http-server .

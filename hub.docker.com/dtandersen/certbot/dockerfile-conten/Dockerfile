FROM ubuntu:14.04
# update package sources
RUN apt-get -y update
RUN apt-get -y upgrade
 
# NVM with default node version installed
RUN apt-get -y install git
 
RUN apt-get -y install build-essential libssl-dev curl
 
RUN git clone https://github.com/creationix/nvm.git /.nvm
 
RUN echo ". /.nvm/nvm.sh" >> /etc/bash.bashrc
RUN echo "/bin/bash -c '. /.nvm/nvm.sh && nvm $1'" > /usr/local/bin/nvm && chmod +x /usr/local/bin/nvm
  
RUN /bin/bash -c '. /.nvm/nvm.sh && nvm install v0.10.20 && nvm use v0.10.20 && nvm alias default v0.10.20 && ln -s /.nvm/v0.10.20/bin/node /usr/bin/node && ln -s /.nvm/v0.10.20/bin/npm /usr/bin/npm'
# forever for running node apps as daemons and automatically restarting on file changes
RUN npm install forever -g
RUN apt-get clean -y

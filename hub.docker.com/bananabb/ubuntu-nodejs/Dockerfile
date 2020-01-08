FROM bananabb/ubuntu-base:base.2.1.0
MAINTAINER BananaBb

#Install Node.js
RUN sudo apt-get update \
 && sudo apt-get install -y \
  	nodejs \ 
  	npm  \
  	build-essential \ 
  	libssl-dev \ 
  	libmysqlclient-dev

# `NVM`(node.js version manager)
ENV NVM_DIR $HOME/.nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.33.8/install.sh | bash \
	&& [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" \ 
	&& [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" \  
    && nvm install 10.16.0 \
    && nvm alias default 10.16.0 \
    && nvm use default

# Install library for Node.js
RUN npm install -g \ 
	pm2 \ 
	sass \
  express-generator \
  create-react-library

# Create working DirectoryRUN /bin/bash -c "
RUN mkdir -p \ 
	/var/www
WORKDIR /var/www

EXPOSE 80 443

CMD ["/bin/bash"]
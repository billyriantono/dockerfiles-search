FROM node:6

LABEL maintainer "Diwakar Cherukumilli"

ENV REFRESHED_AT 2017-12-04

# Install chrome to run the tests
RUN apt-get update && \
    apt-get install -y curl && \
    curl -sL https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    echo 'deb http://dl.google.com/linux/chrome/deb/ stable main' >> /etc/apt/sources.list.d/google.list && \
    apt-get update && \
    apt-get install -y google-chrome-stable

# Disable chrome's sandboxing, because it breaks in Docker.
RUN CHROME_FILE=`which google-chrome` && \
    mv $CHROME_FILE "$CHROME_FILE"-noargs && \
    echo "#!/bin/bash \ngoogle-chrome-noargs --no-default-browser-check --no-sandbox --no-first-run \"\$@\"" > $CHROME_FILE && \
    chmod +x $CHROME_FILE

# RUN apt-get install -y curl xvfb git && \
#     curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh | bash && \
#     export NVM_DIR="$HOME/.nvm" && \
#     [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" && \
#     [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" && \
#     nvm install --lts=boron

# RUN apt-get install -y curl xvfb git && \
#     curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - && \
#     sudo apt-get install -y nodejs

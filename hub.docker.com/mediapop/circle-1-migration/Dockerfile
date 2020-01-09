FROM circleci/python:2.7.15-stretch

RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash - && \
    sudo apt-get install -y nodejs

# Install Yarn.
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && \
    sudo apt-get update && sudo apt-get install yarn

# install chrome for tests
RUN cd /tmp ;\
    wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb &&\
    (sudo dpkg -i google-chrome*.deb || sudo apt-get -f install) &&\
    rm google-chrome*.deb

FROM buildpack-deps:stretch

LABEL amuletkeep=true

COPY ./entrypoint.sh /entrypoint.sh
COPY ./build.sh /build.sh

SHELL ["/bin/bash", "-c"]

ENV DEBIAN_FRONTEND noninteractive

# add user, install rvm nvm
RUN apt-get update && \
    apt-get install --no-install-recommends -y git apt-transport-https locales build-essential && \
    localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8 && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install --no-install-recommends yarn -y && \
    export PATH="/root/.rbenv/bin:/root/.rbenv/shims:$PATH" && \
    curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-installer | bash && \
    echo 'export PATH="/root/.rbenv/bin:/root/.rbenv/shims:$PATH"' >> ~/.bashrc && \
    curl -L https://git.io/n-install > n-install && chmod +x n-install && \
    N_PREFIX=/usr/local/n ./n-install -y && \
    rm n-install && \
    curl -sSL https://git.io/g-install > g-install && chmod +x g-install && \
    echo 'y' | GOROOT=/usr/local/go GOPATH=$HOME/.go ./g-install && \
    rm g-install && \
    curl https://pyenv.run | bash && \
    echo 'export PATH="/root/.pyenv/bin:$PATH"' >> ~/.bashrc && \
    echo 'eval "$(pyenv init -)"' >> ~/.bashrc && \
    echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc && \
    curl -L https://github.com/gohugoio/hugo/releases/download/v0.53/hugo_extended_0.53_Linux-64bit.deb > hugo_extended_0.53_Linux-64bit.deb && \
    dpkg -i ./hugo_extended_0.53_Linux-64bit.deb && \
    rm hugo_extended_0.53_Linux-64bit.deb && \
    source ~/.bashrc && \
    pyenv install 3.7.2 && \
    pyenv install 3.6.8 && \
    pyenv install 3.5.6 && \
    pyenv install 2.7.15 && \
    pyenv global 2.7.15 && \
    g install 1.7 && \
    g install 1.11 && \
    n 8 && \
    n 10 && \
    rbenv install 2.6.0 && \
    rbenv install 2.5.3 && \
    rbenv install 2.4.4 && \
    rbenv global 2.6.0 && \
    mkdir /builder

ENV LANG en_US.UTF-8

WORKDIR /builder
ENTRYPOINT [ "/entrypoint.sh" ]
CMD [ "/build.sh" ]

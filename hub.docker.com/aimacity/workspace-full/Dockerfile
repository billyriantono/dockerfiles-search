FROM buildpack-deps:cosmic

### base ###
RUN yes | unminimize \
    && apt-get install -yq \
        asciidoctor \
        bash-completion \
        build-essential \
        htop \
        jq \
        less \
        llvm \
        locales \
        man-db \
        nano \
        software-properties-common \
        sudo \
        vim \
    && locale-gen en_US.UTF-8 \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/*
ENV LANG=en_US.UTF-8

### Aima user ###
# '-l': see https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#user
RUN useradd -l -u 1000 -G sudo -md /home/aima -s /bin/bash -p aima aima \
    # passwordless sudo for users in the 'sudo' group
    && sed -i.bkp -e 's/%sudo\s\+ALL=(ALL\(:ALL\)\?)\s\+ALL/%sudo ALL=NOPASSWD:ALL/g' /etc/sudoers
ENV HOME=/home/aima
WORKDIR $HOME
# custom Bash prompt
RUN { echo && echo "PS1='\[\e]0;\u \w\a\]\[\033[01;32m\]\u\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\] \\\$ '" ; } >> .bashrc

### C/C++ ###
RUN curl -fsSL https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - \
    && apt-add-repository -yu "deb http://apt.llvm.org/cosmic/ llvm-toolchain-cosmic-6.0 main" \
    && apt-get install -yq \
        clang-format-6.0 \
        clang-tools-6.0 \
        cmake \
    && ln -s /usr/bin/clangd-6.0 /usr/bin/clangd \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/*

### PHP ###
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -yq \
        composer \
        php \
        php-all-dev \
        php-ctype \
        php-curl \
        php-date \
        php-gd \
        php-gettext \
        php-intl \
        php-json \
        php-mbstring \
        php-mysql \
        php-net-ftp \
        php-pgsql \
        php-sqlite3 \
        php-tokenizer \
        php-xml \
        php-zip \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/*
# PHP language server is installed by theia-php-extension

### aima user (2) ###
USER aima
#ENV http_proxy=http://192.168.2.120:7777 
#ENV https_proxy=http://192.168.2.120:7777 
# use sudo so that user does not get sudo usage info on (the first) login
RUN sudo echo "Running 'sudo' for Aima: success"
### Go ###
ENV GO_VERSION=1.12 \
    GOPATH=$HOME/go-packages \
    GOROOT=$HOME/go
ENV PATH=$GOROOT/bin:$GOPATH/bin:$PATH
RUN  curl -fsSL http://aima.hyitec.com/go$GO_VERSION.linux-amd64.tar.gz | tar -xzv \
# install VS Code Go tools: https://github.com/Microsoft/vscode-go/blob/058eccf17f1b0eebd607581591828531d768b98e/src/goInstallTools.ts#L19-åL45
    &&    go get -u -v \
    github.com/mdempsky/gocode \
    github.com/uudashr/gopkgs/cmd/gopkgs \
    github.com/ramya-rao-a/go-outline \
    github.com/acroca/go-symbols \
    github.com/golang/tools/cmd/guru \
    github.com/golang/tools/gorename \
    github.com/fatih/gomodifytags \
    github.com/haya14busa/goplay/cmd/goplay \
    github.com/josharian/impl \
    github.com/tylerb/gotype-live \
    github.com/rogpeppe/godef \
    github.com/zmb3/gogetdoc \
    github.com/golang/tools/cmd/goimports \
    github.com/sqs/goreturns \
    winterdrache.de/goformat/goformat \
    github.com/golang/lint/golint \
    github.com/cweill/gotests/... \
    github.com/alecthomas/gometalinter \
    honnef.co/go/tools/... \
    github.com/golangci/golangci-lint/cmd/golangci-lint \
    github.com/mgechev/revive \
    github.com/sourcegraph/go-langserver \
    github.com/go-delve/delve/cmd/dlv \
    github.com/davidrjenni/reftools/cmd/fillstruct \
    github.com/godoctor/godoctor ; exit 0 && \
    go get -u -v -d github.com/stamblerre/gocode; exit 0 && \
    go build -o $GOPATH/bin/gocode-gomod github.com/stamblerre/gocode && \
    rm -rf $GOPATH/src && \
    rm -rf $GOPATH/pkg
# user Go packages
ENV GOPATH=/workspace/go \
    PATH=/workspace/go/bin:$PATH

### Java ###
## Place '.gradle' and 'm2-repository' in /workspace because (1) that's a fast volume, (2) it survives workspace-restarts and (3) it can be warmed-up by pre-builds.
RUN curl -s "https://get.sdkman.io" | bash \
 && bash -c ". ${HOME}/.sdkman/bin/sdkman-init.sh \
             && sdk install java 8.0.202-zulufx \
             #&& sdk install java 11.0.2-zulufx \
             #&& sdk install java 12.0.1-open \
             && sdk default java 8.0.202-zulufx \
             && sdk install gradle \
             && sdk install maven \
             && mkdir $HOME/.m2 "
  #           "&& printf '<settings>\n  <localRepository>/workspace/.m2/</localRepository>\n</settings>\n' > $HOME/.m2/settings.xml"
ENV GRADLE_USER_HOME=/workspace/.gradle/
ENV JAVA_HOME=$HOME/.sdkman/candidates/java/current
ENV M2_HOME=$HOME/.sdkman/candidates/maven/current

### Node.js ###
ARG NODE_VERSION=10.15.3
#ARG NODE_VERSION=8.16.0

RUN curl -fsSL https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash 
RUN echo 'export NVM_DIR="$HOME/.nvm"'                                       >> "$HOME/.bashrc"
RUN echo '[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm' >> "$HOME/.bashrc"
RUN echo '[ -s "$NVM_DIR/bash_completion" ] && . "$NVM_DIR/bash_completion" # This loads nvm bash_completion' >> "$HOME/.bashrc"

# nodejs and tools
RUN bash -c 'source $HOME/.nvm/nvm.sh   && nvm install $NODE_VERSION     > /dev/null &2>1   '

ENV PATH=$HOME/.nvm/versions/node/v${NODE_VERSION}/bin:$PATH

RUN npm config set registry https://registry.npm.taobao.org &&\
 npm config set disturl https://npm.taobao.org/dist && \
 npm config set python /usr/bin/python --global  && \
 npm config set python /usr/bin/python  && \
 npm install -g yarn typescript 


# RUN sudo  curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash - \
#   && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - \
#   && echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list \
#   &&  sudo apt-get update && sudo apt-get install -y yarn nodejs \
#   && yarn config set registry https://registry.npm.taobao.org  \
#   && yarn config set disturl https://npm.taobao.org/dist  \
#   && npm config set registry https://registry.npm.taobao.org  \
#   && npm config set disturl https://npm.taobao.org/dist  \
#   && sudo apt-get clean && sudo rm -rf /var/lib/apt/lists/* /tmp/*

### Python ###
ENV PATH=$HOME/.pyenv/bin:$HOME/.pyenv/shims:$PATH
RUN curl  -fsSL https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash \
    && { echo; \
        echo 'eval "$(pyenv init -)"'; \
        echo 'eval "$(pyenv virtualenv-init -)"'; } >> .bashrc \
    && pyenv install 2.7.15 \
    && pyenv install 3.7.2 \
    && pyenv global 2.7.15 3.7.2 \
    && pip2 install --upgrade pip \
    && pip2 install virtualenv pipenv pylint rope flake8 autopep8 pep8 pylama pydocstyle bandit python-language-server[all]==0.25.0 \
    && pip3 install --upgrade pip \
    && pip3 install virtualenv pipenv pylint rope flake8 autopep8 pep8 pylama pydocstyle bandit python-language-server[all]==0.25.0 \
    && rm -rf /tmp/*
# Gitpod will automatically add user site under `/workspace` to persist your packages.
# ENV PYTHONUSERBASE=/workspace/.pip-modules \
#    PIP_USER=yes

### Ruby ###
RUN curl -sSL https://rvm.io/mpapis.asc | gpg --import - \
    && curl -sSL https://rvm.io/pkuczynski.asc | gpg --import - \
    &&  curl  -fsSL https://get.rvm.io | bash -s stable \
    && bash -lc " \
        rvm requirements \
        #&& rvm install 2.4 \
        #&& rvm install 2.5 \
        && rvm install 2.6 \
        && rvm use 2.6 --default \
        && rvm rubygems current \
        && gem install bundler --no-document"
ENV GEM_HOME=/workspace/.rvm

### Rust ###
RUN sudo apt-get update \
    && DEBIAN_FRONTEND=noninteractive sudo apt-get install -yq \
        # Enable Rust static binary builds
        musl \
        musl-dev \
        musl-tools \
    && sudo apt-get clean \
    && sudo rm -rf /var/lib/apt/lists/* /tmp/*

RUN curl -fsSL https://sh.rustup.rs | sh -s -- -y \
    && .cargo/bin/rustup update \
    && .cargo/bin/rustup component add rls-preview rust-analysis rust-src \
    && .cargo/bin/rustup completions bash | sudo tee /etc/bash_completion.d/rustup.bash-completion > /dev/null \
    && .cargo/bin/rustup target add x86_64-unknown-linux-musl
RUN bash -lc "cargo install cargo-watch"

### checks ###
# no root-owned files in the home directory
RUN notOwnedFile=$(find . -not "(" -user aima -and -group aima ")" -print -quit) \
    && { [ -z "$notOwnedFile" ] \
        || { echo "Error: not all files/dirs in $HOME are owned by 'aima' user & group"; exit 1; } }

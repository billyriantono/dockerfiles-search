FROM fedora:latest

ENV ADOTDIR=/usr/local/share/.antigen/ \
    ANTIGEN_HOME=/usr/local/share/antigen \
    EDITOR=nvim \
    EMAIL="" \
    GIT_EDITOR="nvim --noplugin" \
    GIT_PAGER="diff-so-fancy | less --tabs=4 -RFX" \
    GIT_USERNAME="" \
    JDT_LS_HOME=/usr/local/lib/eclipse/jdtls \
    SDKMAN_DIR=/usr/local/lib/.sdkman \
    SHELL=/bin/zsh \
    TERM=xterm-256color \
    TERRAFORM_VERSION=0.12.19

# Install basic packages
RUN dnf install -y --setopt=tsflags= \
    @"C Development Tools and Libraries" \
    @"Development Tools" \
    bat \
    docker \
    docker-compose \
    exa \
    fd-find \
    htop \
    httpie \
    jq \
    man-db \
    man-pages \
    neovim \
    npm \
    procps-ng \
    pipenv \
    python3-ansible-lint \
    python3-devel \
    python3-neovim \
    python3-openshift \
    ripgrep \
    tmux \
    which \
    xclip \
    zip \
    zsh \
  && dnf clean -y all

RUN pip3 --no-cache-dir install \
  anchorecli \
  jsondiff \
  python-language-server

RUN npm install -g --no-audit --no-fund \
  @nestjs/cli \
  @typescript-eslint/eslint-plugin \
  @vue/cli \
  bash-language-server \
  diff-so-fancy \
  dockerfile-language-server-nodejs \
  eslint \
  neovim \
  typescript \
  typescript-language-server \
  vscode-css-languageserver-bin \
  vscode-html-languageserver-bin \
  vue-language-server

# Install Terraform
RUN terraform_version=$(curl -fs https://github.com/hashicorp/terraform/releases/latest | grep -Po "(?<=v)[0-9.]*") \
  && curl -fsL https://releases.hashicorp.com/terraform/${terraform_version}/terraform_${terraform_version}_linux_amd64.zip > terraform.zip \
  && unzip terraform.zip -d /usr/local/bin/ \
  && rm terraform.zip

# Install Eclipse JDT language server
RUN mkdir -p ${JDT_LS_HOME} \
  && curl -fsL https://download.eclipse.org/jdtls/snapshots/jdt-language-server-latest.tar.gz | tar -xz -C ${JDT_LS_HOME}

# Install Antigen
RUN git clone --depth 1 https://github.com/zsh-users/antigen.git ${ANTIGEN_HOME}/

# Install Spacevim as system-wide Neovim config
RUN git clone --depth 1 https://github.com/SpaceVim/SpaceVim.git /etc/xdg/nvim

# Install kubectl
RUN kubectl_version=$(curl -fs https://storage.googleapis.com/kubernetes-release/release/stable.txt) \
  && curl -fsL https://storage.googleapis.com/kubernetes-release/release/${kubectl_version}/bin/linux/amd64/kubectl > /usr/local/bin/kubectl \
  && chmod +x /usr/local/bin/kubectl

# Install Helm
RUN curl -fsL https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash

# Install SDKMAN!
RUN curl -fsL https://get.sdkman.io | bash

# Install relevant sdks
RUN source ${SDKMAN_DIR}/bin/sdkman-init.sh \
  && sdk install java 8.0.232.hs-adpt \
  && sdk install java \
  && sdk install maven \
  && sdk install gradle \
  && sdk flush archives \
  && sdk flush temp

COPY root/ /

# Preinstall standard Antigen plugins
RUN touch /root/.zshrc \
  && zsh /etc/zshrc

# Set user environment variables
ENV HOME=/root
ENV JDT_LS_CACHE=${HOME}/.cache/eclipse/jdtls

# Prime everything so the container is ready at startup
RUN source ${SDKMAN_DIR}/bin/sdkman-init.sh \
  && ln -s /etc/.SpaceVim.d ${HOME}/.SpaceVim.d \
  && ln -s /etc/.editorconfig ${HOME}/.editorconfig \
  && nvim --headless +'call dein#install()' +'UpdateRemotePlugins' +qall

VOLUME ${HOME}
WORKDIR ${HOME}/projects
CMD ["/bin/zsh"]

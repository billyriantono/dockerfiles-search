FROM fedora:31

ENV ADOTDIR=/usr/local/share/.antigen/ \
    ANTIGEN_HOME=/usr/local/share/antigen/ \
    EDITOR=nvim \
    JDT_LS_HOME=/usr/local/lib/eclipse/jdtls \
    SDKMAN_DIR=/usr/local/lib/.sdkman \
    SHELL=/bin/zsh \
    TERM=xterm-256color

RUN dnf install -y --setopt=install_weak_deps=False \
    @"C Development Tools and Libraries" \
    @"Development Tools" \
    ansible \
    docker \
    docker-compose \
    findutils \
    htop \
    jq \
    neovim \
    npm \
    procps-ng \
    pipenv \
    python3-ansible-lint \
    python3-devel \
    python3-neovim \
    python3-openshift \
    tmux \
    virtualenv \
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
  @prettier/plugin-xml \
  @vue/cli \
  bash-language-server \
  dockerfile-language-server-nodejs \
  eslint \
  generator-jhipster \
  neovim \
  prettier \
  prettier-plugin-java \
  tslint \
  typescript \
  typescript-language-server \
  vscode-css-languageserver-bin \
  vscode-html-languageserver-bin \
  vue-language-server

# Install Antigen
ADD https://raw.githubusercontent.com/zsh-users/antigen/master/bin/antigen.zsh ${ANTIGEN_HOME}

RUN mkdir -p ${JDT_LS_HOME} \
  && curl -fsL https://download.eclipse.org/jdtls/snapshots/jdt-language-server-latest.tar.gz | tar -xz -C ${JDT_LS_HOME} \
  && mv ${JDT_LS_HOME}/plugins/org.eclipse.equinox.launcher_*.jar ${JDT_LS_HOME}/plugins/org.eclipse.equinox.launcher.jar

# Install SDKMAN! and relevant sdks
RUN curl -fsL https://get.sdkman.io | bash \
  && source ${SDKMAN_DIR}/bin/sdkman-init.sh \
  && sdk i java 8.0.232-open \
  && sdk i java 11.0.5-open \
  && sdk i maven 3.6.3 \
  && sdk i gradle 6.0.1 \
  && sdk flush archives \
  && sdk flush temp

# Install Terraform
RUN curl -fsL https://releases.hashicorp.com/terraform/0.12.18/terraform_0.12.18_linux_amd64.zip > terraform.zip \
  && unzip terraform.zip -d /usr/local/bin/ \
  && rm terraform.zip

# Install Spacevim as system-wide Neovim config
RUN git clone --depth 1 https://github.com/SpaceVim/SpaceVim.git /etc/xdg/nvim

ENV HOME=/root
ENV JDT_LS_CACHE=${HOME}/.cache/eclipse/jdtls \
    PROJECTS_DIR=${HOME}/projects

COPY fs_root/ /

# Prime everything so the container is ready at startup
RUN source ${SDKMAN_DIR}/bin/sdkman-init.sh \
  && ln -s /etc/.SpaceVim.d ${HOME}/.SpaceVim.d \
  && nvim --headless +'call dein#install()' +'UpdateRemotePlugins' +qall \
  && zsh ${HOME}/.zshrc \
  && mkdir -p ${PROJECTS_DIR}

VOLUME ${HOME}
WORKDIR ${PROJECTS_DIR}

ENTRYPOINT ["entrypoint.sh"]
CMD ["/bin/zsh"]

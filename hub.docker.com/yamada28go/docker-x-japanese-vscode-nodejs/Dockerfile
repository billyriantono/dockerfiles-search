FROM yamada28go/docker-x-japanese-vscode-base:ubuntu_18.04-lts
MAINTAINER yamada28go

ENV DEBIAN_FRONTEND noninteractive

USER root
RUN apt-get update && apt-get upgrade -qy  &&  apt-get install -qy build-essential libssl-dev git man curl

USER dev
ENV HOME /home/dev

# install nvm
RUN rm -rf $HOME/.nvm &&\
    mkdir $HOME/.nvm

ENV NVM_DIR $HOME/.nvm
ENV NODE_VERSION 12.13.1

WORKDIR $HOME
RUN curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash \
    && . $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default

RUN echo 'export NVM_DIR="$HOME/.nvm"' >> $HOME/.bash_profile &&\
    echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm' >> $HOME/.bash_profile 

# J­pÉChreomðCXg[
USER root
RUN sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN apt-get update &&\
    apt-get install -qy google-chrome-stable

# dockeràÅÍIvVðÂ¯È¢Æ®ìµÈ¢ÌÅIvVðÝè·é
# [IvVÌÓ¡]
# no-sandbox : Th{bNX@\ÍdockerÌ@\ÆíéÌÅÍ¸·B
# disable-dev-shm-usage : dockerÌftHg¤LÍ­È¢ÌÅ/tempðgp·éæ¤ÉÝè·é
# [Ql]
# ChromeÌ--disable-dev-shm-usageIvVÉÂ¢Ä
# https://qiita.com/yoshi10321/items/8b7e6ed2c2c15c3344c6
# N®IvV
# http://chrome.half-moon.org/43.html#c776272a
#
USER dev
RUN echo 'alias chrome="google-chrome-stable --no-sandbox --disable-dev-shm-usage"' >> $HOME/.bash_profile

# APTR}hðN[·é
USER root
RUN rm -rf /var/lib/apt/lists/* &&\
    apt-get clean   

EXPOSE 22

USER root
CMD ["/usr/sbin/sshd", "-D"]

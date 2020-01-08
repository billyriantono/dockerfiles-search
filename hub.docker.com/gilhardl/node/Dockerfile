ARG NODE_VERSION=lts
FROM node:$NODE_VERSION

LABEL author="Lucas GILHARD <l.gilhard@gmail.com>"
LABEL description="Docker image for Node.js development"

USER root
   
# SYSTEM SETUP
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
  && apt-get upgrade -y \
  && apt-get install -y --no-install-recommends apt-utils 2>&1 \
  && apt-get install -y lsb-release \
  && apt-get install -y bash bash-completion \
  && apt-get install -y curl apt-transport-https wget \
  && apt-get install -y make g++ \
  && sed -i -e "s/bin\/ash/bin\/bash/" /etc/passwd \
  && echo "PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '" >> ~/.bashrc

# YARN
RUN curl --compressed -o- -L https://yarnpkg.com/install.sh | bash

# NPM SETUP
RUN npm cache verify \
  && echo "unsafe-perm = true" >> ~/.npmrc

# CLEAN UP
RUN apt-get autoremove -y \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /tmp/* /var/cache/apt/* \
  && rm -rf ~/.npm
ENV DEBIAN_FRONTEND=dialog

CMD ["bash"]
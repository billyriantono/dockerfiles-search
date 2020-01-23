FROM node

RUN    set -x \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y emacs-nox inotify-tools sudo \
    && rm -rf /var/lib/apt/lists \
    && usermod -l user node \
    && groupmod -n user node \
    && usermod -d /home/user user \
    && mkdir /home/user \
    && chown -R user:user /home/user \ 
    && rm -fr /home/node \
    && echo 'user:pass' | chpasswd \
    && adduser user sudo \
    && adduser user users \
    && npm install -g create-react-app

USER user
WORKDIR "/project"

# For some reason, yarn progress bar is screwed up.
RUN yarn config set no-progress

CMD ["emacs"]

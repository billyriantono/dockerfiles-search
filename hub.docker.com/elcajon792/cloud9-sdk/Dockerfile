# Cloud9 server

FROM node:8-alpine

RUN apk -U --no-cache --no-progress upgrade \
 && apk -U --no-cache --force --no-progress add bash tmux git make gcc g++ python sqlite wget openssl ca-certificates zip docker zsh \
 && npm config set unsafe-perm true \
 && npm install -g forever && npm cache clean --force \
 && git clone --depth=5 https://github.com/c9/core.git /root/.c9 && cd /root/.c9 \
 && npm install pty.js \
 && mkdir -p ./node/bin ./bin ./node_modules \
 && ln -sf "`which tmux`" ./bin/tmux \
 && ln -s "`which node`" ./node/bin/node \
 && ln -s "`which npm`" ./node/bin/npm \
 && echo 1 > ./installed \
 && NO_PULL=1 ./scripts/install-sdk.sh \
 && npm cache clean --force && rm -rf /var/cache/apk/* /tmp/* /var/tmp/* \
 && git reset --hard \
 && wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh \
 && sed -i -- 's/ZSH_THEME="robbyrussell"/ZSH_THEME="maran"/g' /root/.zshrc \
 && cd /root \
 && wget https://github.com/tmux/tmux/releases/download/2.2/tmux-2.2.tar.gz \
 && tar xzf tmux-2.2.tar.gz \
 && cd /root/tmux-2.2 \
 && apk add libevent-dev ncurses-dev -y \
 && ./configure --prefix="/root/.c9/local" \
 && make \
 && make install \
 && rm /root/.c9/bin/tmux \
 && ln -sf /root/.c9/local/bin/tmux /root/.c9/bin/tmux \
 && cd /root \
 && rm /root/tmux-2.2.tar.gz \
 && rm -r /root/tmux-2.2 



ENV SHELL /bin/zsh
VOLUME /workspace
EXPOSE 8181
#ENV USER c9
#ENV PASSWORD c9
ENTRYPOINT ["forever", "/root/.c9/server.js", "-w", "/workspace", "--listen", "0.0.0.0"]

CMD ["--auth", "c9:c9"] 


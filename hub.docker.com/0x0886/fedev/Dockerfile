FROM node

WORKDIR /webapp

RUN echo 'PS1="${debian_chroot:+($debian_chroot)}\h:\W\$ "' >> /root/.bashrc \
    && echo 'export LS_OPTIONS="--color=auto"' >> /root/.bashrc \
    && echo 'alias ls="ls $LS_OPTIONS"' >> /root/.bashrc \
    && echo 'alias ll="ls $LS_OPTIONS -l"' >> /root/.bashrc \
    && npm set registry https://registry.npm.taobao.org \
    && yarn config set registry https://registry.npm.taobao.org \
    && yarn global add serve

CMD ["bash"]

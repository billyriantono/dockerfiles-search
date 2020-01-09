ARG ALPINE_TAG=3.10
FROM spritsail/alpine:${ALPINE_TAG}

# change default shell from ash to bash
RUN sed -i -e "s/bin\/ash/bin\/bash/" /etc/passwd

# install minimal c++ environment
RUN apk --no-cache add sudo bash bash-completion zsh git\
  gcc g++ gdb libc-dev linux-headers \
  make ninja cmake

ARG USERNAME=vscode

RUN addgroup -S $USERNAME
RUN adduser -S -s /bin/zsh -h /home/$USERNAME -D -G $USERNAME $USERNAME
RUN echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Create VSCode mound for extension. We don't want to re-download and re-install
RUN mkdir -p /home/$USERNAME/.vscode-server/extensions \
  /home/$USERNAME/.vscode-server-insiders/extensions \
  && chown -R $USERNAME \
  /home/$USERNAME/.vscode-server \
  /home/$USERNAME/.vscode-server-insiders

# Persist bash and zsh history
RUN SNIPPET="export HISTFILE=/commandhistory/.zsh_history" \
  && mkdir /commandhistory \
  && touch /commandhistory/.zsh_history \
  && chown -R $USERNAME /commandhistory \
  && echo $SNIPPET >> "/home/$USERNAME/.zshrc" \
  && SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.bash_history" \
  && echo $SNIPPET >> "/root/.bashrc" \
  && touch /commandhistory/.bash_history \
  && chown -R $USERNAME /commandhistory \
  && echo $SNIPPET >> "/home/$USERNAME/.bashrc"

USER ${USERNAME}
# Install oh-my-zsh
RUN cd ~ \
  && sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)" \
  && sudo ln -s .zshrc /root/.zshrc \
  && sudo ln -s .oh-my-zsh /root/.oh-my-zsh

ENTRYPOINT ["/bin/zsh"]
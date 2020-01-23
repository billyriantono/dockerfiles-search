FROM alpine

RUN apk add --no-cache vim fish git bash alpine-sdk the_silver_searcher openssh

# Use my own username
RUN adduser -s /usr/bin/fish -D alan
RUN echo "alan    ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Install fish prompt
COPY config.fish /home/alan/.config/fish/config.fish
COPY fish_prompt.fish /home/alan/.config/fish/functions/fish_prompt.fish
COPY github_init.fish /home/alan/.config/fish/functions/github_init.fish

# Configure vim
COPY vimrc /home/alan/.vimrc
COPY vim/ /home/alan/.vim/
RUN mkdir /home/alan/.vim/swap

# Make sure everything is owned by me
RUN chown -R alan:alan /home/alan

USER alan

# Install vim plugins
RUN vim +PlugInstall +qall

WORKDIR /home/alan
CMD fish

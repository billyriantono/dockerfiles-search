FROM alpine:latest

RUN apk add --update \
git \
linux-headers \
unzip \
the_silver_searcher \
curl \
python \
neovim \
python-dev \
bash \
gcc \
make \
go \
zsh \
tmux \
docker \
musl-dev \
openssh-client \
mosh-server \
ca-certificates \
&& rm -rf /var/cache/apk/*

# install neovim plugins
RUN apk add --update-cache --no-cache git python3 && \
apk add --no-cache --virtual build-deps musl-dev gcc python3-dev && \
python3 -m ensurepip && \
pip3 install --upgrade pip setuptools && \
pip3 install neovim && \
curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

RUN mkdir -p ~/.config/nvim/plugged
COPY ./init.vim /root/.config/nvim/init.vim

RUN nvim --headless -c "PlugInstall! | qall! " && \
nvim --headless +UpdateRemotePlugins +qall

# install zsh
RUN sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
RUN rm -f ~/.zshrc

# my dot files
RUN cd /root && git clone https://github.com/andre-karrlein/dot-ak1.git
RUN ln -s /root/dot-ak1/tmux.conf ~/.tmux.conf && ln -s /root/dot-ak1/zshrc ~/.zshrc
RUN git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions


# install gotests
RUN cd /root/go/bin && go get -u github.com/cweill/gotests/...

# create code dir
RUN mkdir /root/code
WORKDIR /root
RUN sed -i 's/ash/zsh/g' /etc/passwd

# install kubectl
RUN curl -L -o /usr/local/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
RUN chmod 755 /usr/local/bin/kubectl

ENV LANG="en_US.UTF-8"
ENV LC_ALL="en_US.UTF-8"
ENV LANGUAGE="en_US.UTF-8"

# install gcloud
RUN curl -sSL https://sdk.cloud.google.com | /bin/zsh
ENV PATH $PATH:/root/google-cloud-sdk/bin

RUN git config --global user.email "andre@karrlein.com"
RUN git config --global user.name "Andre Karrlein"

EXPOSE 6001/udp

RUN mosh-server

ENTRYPOINT [ "/bin/zsh" ]

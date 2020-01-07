FROM mikesir87/aws-cli

MAINTAINER packeteer <packeteer@gmail>

RUN apk add --no-cache --update zsh openssh rsync tmux git ansible neovim httpie unzip
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
RUN wget https://releases.hashicorp.com/terraform/0.11.14/terraform_0.11.14_linux_amd64.zip && \
    unzip terraform_0.11.14_linux_amd64.zip -d /usr/local/bin && \
    rm terraform_0.11.14_linux_amd64.zip

COPY ./config/* /root/
ENV SHELL=/bin/zsh
ENV LC_ALL=en_US.UTF-8

ENTRYPOINT ["zsh"]

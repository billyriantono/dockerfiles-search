FROM debian:stretch

RUN apt-get update && apt-get install -y \
    curl \
    git \
    procps \
    sudo \ 
    vim \
    zsh

RUN useradd -m osvaldo && echo "osvaldo:docker" | chpasswd && adduser osvaldo sudo

USER osvaldo

RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

CMD ["zsh"]
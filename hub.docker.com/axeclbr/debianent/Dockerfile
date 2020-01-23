FROM microsoft/azure-cli:latest

LABEL maintainer="Aaron Weiker" \
    org.label-schema.vcs-url="https://github.com/aweiker/azure-cli.git" \
    org.label-schema.docker.cmd="docker run -it --rm -v ${HOME}/.ssh:/home/az/.ssh -v ${HOME}/.azure:/home/az/.azure -v ${HOME}/src:/src aweiker/azure-cli:latest"

RUN apk add --no-cache zsh vim zsh-vcs gnupg && \
    rm /usr/bin/vi && \
    ln  /usr/bin/vim /usr/bin/vi && \
    adduser az az -D -s /bin/zsh && \
    hostname -s azure-cli

USER az:az
WORKDIR /home/az

COPY . /home/az/.install

RUN (/home/az/.install/install-zsh.sh || true) && \
    cp /home/az/.install/zshrc /home/az/.zshrc

CMD zsh

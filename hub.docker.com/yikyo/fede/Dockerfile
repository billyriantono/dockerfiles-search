FROM node:latest

LABEL maintainer="yikyo666@gmail.com"

RUN curl -o /etc/apt/sources.list http://mirrors.163.com/.help/sources.list.jessie

RUN apt-get update && apt-get install -y zsh && rm -rf /var/lib/apt/lists/

RUN git --git-dir=/dev/null clone --depth=1 git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh

RUN cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

RUN sed -i -e 's/robbyrussell/af-magic/' ~/.zshrc

ENTRYPOINT ["/bin/zsh"]

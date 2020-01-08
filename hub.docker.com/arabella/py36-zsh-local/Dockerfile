FROM python:3.6
ENV PYTHONUNBUFFERED 1
ENV TERM xterm
RUN mkdir /www
WORKDIR /www
RUN apt-get update && apt-get -y install apt-utils mysql-client bash-completion zsh git-core memcached
# From here we load our application's code in, therefore the previous docker
# "layer" thats been cached will be used if possible
# Install Zsh
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh \
        && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc \
        && chsh -s /bin/zshrc.zsh-template \ 
        && echo '[[ "$TERM" == "xterm" ]] && export TERM=xterm-256color' >> ~/.zshrc \
        && echo 'source /www/venv/bin/activate' >> ~/.zshrc \
        && echo 'source /www/venv/bin/activate' >> ~/.bashrc

RUN pip install virtualenv


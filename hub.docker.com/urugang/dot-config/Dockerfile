# see dot_build and dot_exec in .bash_profile
FROM ubuntu:17.10


ARG GITHUB_USER=$GITHUB_USER
ARG GITHUB_PASS=$GITHUB_PASS



COPY   . /home/urugang/codes/dot-config
RUN      /home/urugang/codes/dot-config/system-setup.sh

USER     urugang
WORKDIR  /home/urugang

RUN      echo "machine github.com\n\tlogin $GITHUB_USER\n\tpassword $GITHUB_PASS" >> ~/.netrc
RUN      /home/urugang/codes/dot-config/user-setup.sh
RUN      rm -f ~/.netrc
CMD      source ~/.bash_profile; emacs --daemon; /etc/init.d/ssh restart; sleep 25920000000

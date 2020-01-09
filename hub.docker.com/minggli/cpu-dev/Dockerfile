FROM minggli/base-dev

ENV LANG C.UTF-8
SHELL ["/bin/bash", "-c"]

RUN apt-get update
RUN apt-get install -qqy tmux vim software-properties-common sudo

RUN apt-add-repository -y ppa:cpick/hub && \
    apt-add-repository -y ppa:keithw/mosh
RUN apt-get update && apt-get install -qqy tmate hub mosh iptables openssh-server pwgen supervisor

RUN mkdir ~/bin
RUN cd ~/bin && git clone https://github.com/minggli/dotfiles.git
RUN touch ~/.bashrc && echo ". ~/bin/dotfiles/bashrc" >> ~/.bashrc
RUN touch ~/.bash_profile && echo ". ~/.bashrc" >> ~/.bash_profile && \
    /bin/bash -c "source ~/.bash_profile"

RUN sudo curl -o /usr/local/bin/rmate https://raw.githubusercontent.com/aurora/rmate/master/rmate && sudo chmod +x /usr/local/bin/rmate

RUN echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config && echo "PermitRootLogin yes" >> /etc/ssh/sshd_config

RUN echo "eval \$(ssh-agent -s) > /dev/null " >> ~/.bashrc

ADD start.sh /start.sh

CMD /start.sh

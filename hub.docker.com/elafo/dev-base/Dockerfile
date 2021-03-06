FROM ubuntu:17.10
MAINTAINER eLafo

#### DEVELOPMENT ENVIRONMENT CONFIGURATION #####
ENV APP_HOME=/workspace

###### USER CREATION #########
ENV USER_NAME=dev
ENV USER_HOME=/home/$USER_NAME

ENV PATH $USER_HOME:$PATH

RUN mkdir $APP_HOME
######### GENERAL DEVELOPMENT LIBRARIES AND TOOLS #########

RUN apt-get update &&\
    echo "debconf debconf/frontend select Teletype" | debconf-set-selections && apt-get install -y -qq --no-install-recommends\
      vim\
      sudo\
      git\
      curl\
      wget\
      redis-tools\
      build-essential\
      ruby\
      software-properties-common\
      bash-completion\
      silversearcher-ag\
      libpq-dev\
      tzdata\
      libxml2-dev\
      libxslt-dev\
      ssh\
      postgresql\
      postgresql-contrib\
      nmap\
      net-tools\
      libarchive-dev\
      libodbc1\
      mysql-client\
      libmysqlclient-dev\
      cmake\
      chrpath\
      libssl-dev\
      libxft-dev\
      libfreetype6\
      libfreetype6-dev\
      libfontconfig1\
      libfontconfig1-dev\
      exuberant-ctags

# Install Homesick, through which dotfiles configurations will be installed
RUN gem install homesick --no-rdoc --no-ri

######### SSH ########

# Install the Github Auth gem, which will be used to get SSH keys from GitHub
# to authorize users for SSH
RUN gem install github-auth --no-rdoc --no-ri

# Set up SSH. We set up SSH forwarding so that transactions like git pushes
# from the container happen magically.
RUN apt-get install -y openssh-server -qq --no-install-recommends &&\
    mkdir /var/run/sshd &&\
    echo "AllowAgentForwarding yes" >> /etc/ssh/sshd_config &&\
    echo "PermitUserEnvironment yes" >> /etc/ssh/sshd_config

# Expose SSH
EXPOSE 22

# Setting locale
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen &&\
    sed -i -e 's/# es_ES.UTF-8 UTF-8/es_ES.UTF-8 UTF-8/' /etc/locale.gen

RUN locale-gen en_US.UTF-8 es_ES.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN useradd $USER_NAME -d $USER_HOME -m -s /bin/bash &&\
    adduser $USER_NAME sudo && \
    echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

RUN mkdir $USER_HOME/.ssh
########## TERMINAL ##########

# Config TERM
ENV TERM=screen-256color

# Install tmux
RUN apt-get install -y -qq --no-install-recommends libevent-dev libncurses-dev
RUN cd /tmp && wget https://github.com/tmux/tmux/releases/download/2.4/tmux-2.4.tar.gz 
RUN cd /tmp && tar -zxvf /tmp/tmux-2.4.tar.gz && cd /tmp/tmux-2.4 && ./configure && make && make install

# Install wemux
RUN git clone git://github.com/zolrath/wemux.git /usr/local/share/wemux &&\
    ln -s /usr/local/share/wemux/wemux /usr/local/bin/wemux &&\
    cp /usr/local/share/wemux/wemux.conf.example /usr/local/etc/wemux.conf &&\
    echo "host_list=(dev)" >> /usr/local/etc/wemux.conf

COPY ssh_key_adder.rb /home/dev/ssh_key_adder.rb 
COPY ssh_start.sh /home/dev/ssh_start.sh

###### USER CONFIGURATION #######
RUN chown -R $USER_NAME:$USER_NAME $USER_HOME $APP_HOME &&\
    chmod +x /home/dev/ssh_key_adder.rb &&\
    chmod +x /home/dev/ssh_start.sh 

USER $USER_NAME

# Dotfiles

RUN \
# Set up The Editor of the Gods
    homesick clone https://github.com/eLafo/vim-dot-files.git &&\
    homesick symlink vim-dot-files &&\
    exec vim -c ":PluginInstall" -c "qall"

RUN \
    homesick clone eLafo/git-dot-files &&\
    homesick symlink git-dot-files

RUN \
    homesick clone eLafo/bash-dot-files &&\
    homesick symlink --force=true bash-dot-files

RUN \
    homesick clone eLafo/tmux-dot-files &&\
    homesick symlink --force=true tmux-dot-files

VOLUME $APP_HOME

WORKDIR $APP_HOME

CMD bash

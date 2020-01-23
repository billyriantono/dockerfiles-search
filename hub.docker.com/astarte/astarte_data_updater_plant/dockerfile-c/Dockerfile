FROM ubuntu:16.04
MAINTAINER ASPgems

# Start by changing the apt otput, as stolen from Discourse's Dockerfiles.
RUN echo "debconf debconf/frontend select Teletype" | debconf-set-selections &&\
# Probably a good idea
    apt-get update &&\

# Basic dev tools
    apt-get install -y sudo openssh-client git build-essential vim ctags man curl direnv software-properties-common

# Set up for pairing with wemux.
RUN apt-get install -y tmux &&\
    git clone git://github.com/zolrath/wemux.git /usr/local/share/wemux &&\
    ln -s /usr/local/share/wemux/wemux /usr/local/bin/wemux &&\
    cp /usr/local/share/wemux/wemux.conf.example /usr/local/etc/wemux.conf &&\
    echo "host_list=(dev)" >> /usr/local/etc/wemux.conf

# Install neovim
RUN add-apt-repository ppa:neovim-ppa/stable &&\
    apt-get update &&\
    apt-get install -y neovim
# RUN add-apt-repository ppa:neovim-ppa/unstable &&\
#     apt-get update &&\
#     apt-get install neovim

# Install Homesick, through which zsh and vim configurations will be installed
RUN apt-get install -y ruby &&\
    gem install homesick --no-rdoc --no-ri

# Install the Github Auth gem, which will be used to get SSH keys from GitHub
# to authorize users for SSH
RUN gem install github-auth --no-rdoc --no-ri

# Install zsh
RUN apt-get install -y zsh

# Install a couple of helpful utilities
RUN apt-get install -y ack-grep &&\
    gem install git-duet --no-rdoc --no-ri

# Set up SSH. We set up SSH forwarding so that transactions like git pushes
# from the container happen magically.
RUN apt-get install -y openssh-server &&\
    mkdir /var/run/sshd &&\
    echo "AllowAgentForwarding yes" >> /etc/ssh/sshd_config

# Fix for occasional errors in perl stuff (git, ack) saying that locale vars
# aren't set.
# RUN locale-gen en_US en_US.UTF-8 && dpkg-reconfigure locales

RUN useradd dev -d /home/dev -m -s /bin/zsh &&\
    adduser dev sudo && \
    echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

COPY ssh_key_adder.rb /home/dev/ssh_key_adder.rb
RUN chown dev:dev /home/dev/ssh_key_adder.rb &&\
    chmod +x /home/dev/ssh_key_adder.rb

USER dev
WORKDIR /home/dev

RUN \
# Set up shell
    homesick clone dpetersen/zshfiles &&\
    homesick symlink zshfiles &&\

# Set up The Editor of the Gods
    homesick clone dpetersen/vimfiles &&\
    homesick symlink vimfiles &&\
    cd ~/.vim/bundle_storage/vimproc.vim && make &&\

# Set up neovim
    mkdir ~/.config &&\
    ln -s ~/.vim ~/.config/nvim &&\
    ln -s ~/.vimrc ~/.config/nvim/init.vim

# Expose SSH
EXPOSE 22

# Install the SSH keys of ENV-configured GitHub users before running the SSH
# server process. See README for SSH instructions.
CMD /home/dev/ssh_key_adder.rb && sudo /usr/sbin/sshd -D

############################################################
# Dockerfile to build OhMyZsh container images
# Based on Latest CentOS
############################################################

# Set the base image to CentOS
FROM centos:6.6

# File Author / Maintainer
MAINTAINER Ben Withem

#RUN rpm -ivh http://mirrors.opencas.cn/epel/6/i386/epel-release-6-8.noarch.rpm
RUN rpm -ivh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm

ENV HOME /root
RUN yum -y update
RUN yum install -y zsh git tmux openssh-server vim wget tar gcc
RUN ssh-keygen -N '' -t rsa -q -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -N '' -t dsa -q -f /etc/ssh/ssh_host_dsa_key
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
RUN echo hello|passwd --stdin root
RUN sed -i -E "s/UsePAM yes/#UsePAM yes/" /etc/ssh/sshd_config
RUN sed -i -E "s/#UsePAM no/UsePAM no/" /etc/ssh/sshd_config


################## BEGIN INSTALLATION ######################
RUN git clone git://github.com/bwithem/oh-my-zsh.git ~/.oh-my-zsh \
    && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc \
    && chsh -s /bin/zsh
RUN sed -i -E "s/^plugins=\((.*)\)$/plugins=(\1 tmux themes tmuxinator)/" ~/.zshrc

RUN yum install -y ruby ruby-devel rubygems rpm-build
RUN gem sources --remove https://rubygems.org/
RUN gem sources -a http://ruby.taobao.org/
RUN gem update --system
RUN gem install tmuxinator
WORKDIR /root
CMD ["/usr/sbin/sshd","-D"]

####### vim #############
git clone https://github.com/gmarik/vundle.git ~/.vim/bundle/vundle
git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim`

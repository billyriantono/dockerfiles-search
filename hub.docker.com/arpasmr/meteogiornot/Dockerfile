FROM centos:centos7

MAINTAINER arnow117 "arnow117@gmail.com"
ENV TOOLS_PATH /root/Tools
ENV WORK_PATH /root/Workspace
RUN mkdir $TOOLS_PATH $WORK_PATH

RUN yum install -y https://centos7.iuscommunity.org/ius-release.rpm
RUN yum install -y epel-release git vim wget python python36u python36u-libs python36u-devel python36u-pip tmux openssh-server zsh man-pages man-db man
RUN pip3.6 install ipython
RUN ln -s /usr/bin/python3.6 /usr/bin/python3
RUN echo "install essential basic apps"

#Config awesome vim
RUN git clone --depth=1 git://github.com/amix/vimrc.git ~/.vim_runtime
RUN sh ~/.vim_runtime/install_basic_vimrc.sh

#Install&config oh-my-zsh
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
RUN chsh -s /bin/zsh
COPY zshrc /root/.zshrc

#Config PIP for China & install IPython
RUN mkdir -p /root/.config/pip
COPY pip.conf /root/.config/pip/pip.conf

#Config default sshd
RUN mkdir /var/run/sshd
RUN echo 'root:toor' |chpasswd
RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
EXPOSE 22/tcp
CMD ["/usr/sbin/sshd","-D"]

WORKDIR $WORK_PATH


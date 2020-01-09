FROM archlinux:20191105

LABEL maintainer="hayicle.vn@gmail.com"
LABEL version="1.0"
LABEL description="vim IDE"

USER root

ENV PASSWORD='drowssap'

#install needed packages
RUN pacman -Sy --noconfirm neovim git openssh && \
    mkdir -p /root/.config/nvim/ && \
    curl -fLo /root/.local/share/nvim/site/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim 

#Config ssh
RUN /usr/bin/ssh-keygen -A && \
  sed -i 's/#PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
  echo -e "$PASSWORD\n$PASSWORD" | passwd root

#Config nvim
ADD conf/init.vim /root/.config/nvim/init.vim

#Install Plugin nvim
RUN nvim +'PlugInstall' +'q!' +'q!' && \
    echo "alias vim='nvim'" >> /root/.bashrc

EXPOSE 22

CMD ["/usr/sbin/sshd","-D"]

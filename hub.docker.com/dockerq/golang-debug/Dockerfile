FROM golang:1.7.4
MAINTAINER adolphlwq kenan@3015@gmail.com
ENV TERM dumb
RUN ln -f -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN apt-get update && \
    apt-get install -y --no-install-recommends supervisor git vim && \
    git clone https://github.com/amix/vimrc.git ~/.vim_runtime && sh ~/.vim_runtime/install_awesome_vimrc.sh && \
    apt-get clean
ADD supervisord.conf /etc/supervisord.conf
CMD ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]

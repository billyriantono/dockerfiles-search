FROM alpine:3.4
MAINTAINER pkhanhao <pkhanhao@163.com>

RUN echo "===> Install system packages..." && \
        echo -e "http://mirrors.ustc.edu.cn/alpine/v3.4/main\nhttp://mirrors.ustc.edu.cn/alpine/v3.4/community" > /etc/apk/repositories && \
        apk update && \
        apk add openssh openssh-sftp-server ruby ruby-dev ruby-bundler ruby-irb ruby-rdoc build-base libffi-dev && \
        rm -rf /var/cache/apk/* && \
    echo "===> Gem install jekyll..." && \
        gem sources --add http://gems.ruby-china.org/ --remove https://rubygems.org/ && \
        bundle config mirror.https://rubygems.org http://gems.ruby-china.org && \
        gem install jekyll && \
    echo "===> For user and passwd..." && \
        echo 'root:jekyll' | chpasswd && \
    echo "===> Initialize sshd.." && \
        mkdir /var/run/sshd && \
        ssh-keygen -A && \
        echo -e "Port 22\nProtocol 2\nPermitRootLogin yes\nChallengeResponseAuthentication no\nPasswordAuthentication yes\nX11Forwarding yes\nPrintMotd no\nAcceptEnv LANG LC_*\nSubsystem sftp /usr/lib/ssh/sftp-server\nLogLevel VERBOSE\nUseDNS no" > /etc/ssh/sshd_config

EXPOSE 22
EXPOSE 4000
CMD ["/usr/sbin/sshd","-D"]

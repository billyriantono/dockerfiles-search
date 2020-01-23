FROM centos:latest
MAINTAINER ilpan<pna110@126.com>

WORKDIR /root/

RUN yum install -y unzip which tar sudo net-tools \ 
        openssh-server openssh-clients rsync && \ 
        yum clean all

# install jenv
RUN curl -L -s get.jenv.io | bash && \ 
        source "/root/.jenv/bin/jenv-init.sh" && \ 
        jenv selfupdate && jenv config auto true && \ 
        mv /root/.jenv /usr/local/ && ln -s /usr/local/.jenv /root/.jenv

RUN  source "/root/.jenv/bin/jenv-init.sh" && \ 
        jenv install java 1.8.0_112 && \ 
        rm -rf /usr/local/.jenv/archives/*

# ssh service
RUN ssh-keygen -t rsa -P '' -f /etc/ssh/ssh_host_rsa_key && \ 
        ssh-keygen -t ecdsa -P '' -f /etc/ssh/ssh_host_ecdsa_key && \
        ssh-keygen -t ed25519 -P '' -f /etc/ssh/ssh_host_ed25519_key 

# login withou password
RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
RUN cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
        chmod 700 ~/.ssh && \
        chmod 644 ~/.ssh/authorized_keys


EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]

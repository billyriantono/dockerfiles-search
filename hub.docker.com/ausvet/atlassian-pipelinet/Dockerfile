FROM julia:1.1
MAINTAINER Aurelio Amerio

RUN apt-get update &&\
    apt-get install -y bzip2 wget gnupg dirmngr apt-transport-https ca-certificates openssh-server tmux locales&&\
    apt-get -y -u install hdf5-tools &&\
    apt-get clean

COPY install_packages.jl /tmp/install_packages.jl

RUN julia /tmp/install_packages.jl

RUN mkdir /var/run/sshd

RUN echo 'root:u33dcUtnDELPB3e4UGSTg2BVArkz' |chpasswd

RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

RUN mkdir /root/.ssh

RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]

#add support for English and Italian
COPY locale.gen /etc/locale.gen
RUN locale-gen

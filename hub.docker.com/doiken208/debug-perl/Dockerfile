FROM centos/tools
MAINTAINER ryugaku2008

ARG version="5.24.4"
ENV container docker
LABEL RUN="docker run -it --name NAME --privileged  —cap-add=SYS_PTRACE —security-opt='seccomp=unconfined' --ipc=host --net=host --pid=host -e HOST=/host -e NAME=NAME -e IMAGE=IMAGE -v /sys/fs/selinux:/sys/fs/selinux:ro -v /run:/run -v /var/log:/var/log -v /etc/localtime:/etc/localtime -v /:/host IMAGE"

# Swap out the systemd-container package and install all useful packages
RUN yum -y install \
           patch \
           && yum clean all

RUN yum -y reinstall "*" && yum clean all

RUN curl -L http://install.perlbrew.pl | bash
ENV PATH $PATH:/root/perl5/perlbrew/bin/
RUN echo "source ~/perl5/perlbrew/etc/bashrc" >> ~/.bash_profile

RUN perlbrew install --notest ${version} --as=perl-${version}-gO0 -DDEBUGGING=-g -Doptimize=-O0
RUN bash -lc 'perlbrew switch perl-${version}-gO0'

RUN debuginfo-install -y glibc-2.17-260.el7.x86_64 nss-softokn-freebl-3.36.0-5.el7_5.x86_64
COPY .gdbinit /root/.gdbinit

RUN bash -lc '\
cpan install \
  Term::ReadKey \
  inc/Module/Install.pm \
  Module/Install/XSUtil.pm \
  Module/Install/AuthorTests.pm \
&& cpan install -T \
  Term::ReadLine::Perl'

# Set default command
CMD ["/usr/bin/bash", "-l"]

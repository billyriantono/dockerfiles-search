FROM ubuntu:latest
MAINTAINER = Jason M. Mills <jmmills@cpan.org>
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get install -y cpanminus
RUN apt-get install -y libfcgi-procmanager-perl
RUN apt-get install -y build-essential
RUN apt-get install -y git
ADD install_gitalist_apt_deps.sh /tmp/install_gitalist_apt_deps.sh
RUN /bin/sh /tmp/install_gitalist_apt_deps.sh
RUN cpanm -n Gitalist
RUN rm -v /tmp/install_gitalist_apt_deps.sh

EXPOSE 3000
CMD ["/usr/local/bin/gitalist_server.pl"]

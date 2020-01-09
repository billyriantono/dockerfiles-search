FROM jmmills/minicpan:latest
MAINTAINER = Jason M. Mills <jmmills@cpan.org>
ENV DEBIAN_FRONTEND noninteractive
RUN minicpan -l /cpan/ --remote-from cpan

ADD cpan /cpan
RUN apt-get install -y nginx

ENTRYPOINT ["/bin/bash"]
CMD ["-l"]

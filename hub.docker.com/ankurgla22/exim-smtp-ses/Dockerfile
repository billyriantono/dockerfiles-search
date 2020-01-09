FROM oraclelinux
MAINTAINER ankurgla22@gmail.com

RUN yum update -y \
    && yum install -y exim4 \
    && service sendmail stop \
    && service exim start \
    && chkconfig exim on \
    && chkconfig sendmail off \
    && rm /etc/exim/exim.conf



COPY exim.conf /etc/exim5


RUN service exim restart

EXPOSE 25/tcp
CMD ["app:start"]

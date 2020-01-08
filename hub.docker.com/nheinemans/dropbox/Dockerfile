FROM centos
MAINTAINER Nick Heinemans (nick@hostlogic.nl)
RUN yum install -y python tar \
&& yum clean all

RUN cd /home \
&& curl -L -s "https://www.dropbox.com/download?plat=lnx.x86_64" | tar -xz

RUN curl -L -s https://www.dropbox.com/download?dl=packages/dropbox.py -o /bin/dropbox.py \
&& chmod +x /bin/dropbox.py

ENTRYPOINT /home/.dropbox-dist/dropboxd

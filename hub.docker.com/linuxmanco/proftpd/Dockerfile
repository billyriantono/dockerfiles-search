FROM ubuntu

RUN apt update -y
RUN apt install -y proftpd

ADD proftpd.conf /etc/proftpd/proftpd.conf
ADD passwd /etc/proftpd/auth/passwd
RUN chown root:root /etc/proftpd/auth/passwd
RUN groupadd ftp
RUN chown root:root /etc/proftpd/proftpd.conf
RUN mkdir /ftp

EXPOSE 21
EXPOSE 20
EXPOSE 40000
EXPOSE 40001

RUN useradd -s /bin/bash -d /ftp defaultuser
RUN usermod -G defaultuser defaultuser
RUN echo 'defaultuser:defaultuser' | chpasswd
RUN usermod -G users defaultuser
RUN chown defaultuser:users /ftp -R

CMD ["proftpd", "--nodaemon", "-c", "/etc/proftpd/proftpd.conf"]
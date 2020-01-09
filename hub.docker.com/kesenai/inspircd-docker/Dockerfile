FROM debian:latest

MAINTAINER K7R2EFZA@protonmail.com

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y inspircd

RUN adduser user
RUN mkdir /usr/lib/inspircd/logs/
RUN chown -R user /usr/lib/inspircd/

RUN rm /etc/inspircd/inspircd.conf
COPY ./conf/inspircd.conf /etc/inspircd/

RUN chown -R user /etc/inspircd
RUN touch /var/run/inspircd.pid
RUN chown user /var/run/inspircd.pid

EXPOSE 6667/tcp

ENTRYPOINT [ "/bin/su", "-m", "user", "-c", "/usr/sbin/inspircd start --nofork >/dev/null 2>&1" ]


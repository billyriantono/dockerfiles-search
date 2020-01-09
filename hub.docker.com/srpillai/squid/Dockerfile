FROM ubuntu
MAINTAINER s.r.pillai@in.ibm.com
RUN apt-get update && apt-get install squid -y
EXPOSE 8888/tcp
CMD [ "squid3","-f","/etc/squid/squid.conf","-NYCd","1" ]

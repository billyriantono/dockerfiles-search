FROM frolvlad/alpine-mono
MAINTAINER https://github.com/einsz

RUN mkdir /intersect
COPY files/ /intersect/
WORKDIR /intersect

CMD [ "mono",  "./Intersect Server.exe" ]
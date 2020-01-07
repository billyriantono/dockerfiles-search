FROM httpd:alpine

MAINTAINER Joaquín Rufo Gutierrez (joaquinito01@youtube.com)

RUN apk update

RUN apk add python python-dev py-pip build-base

RUN cd /usr/local/apache2/htdocs/

RUN pip install internetarchive

EXPOSE 80

CMD ["python","ia-collection-dl.py","archiveteam_youtube"]

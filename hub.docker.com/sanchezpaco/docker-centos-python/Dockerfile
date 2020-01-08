FROM centos:7
MAINTAINER "Paco Sanchez" <sanchezpaco3@gmail.com>
RUN yum update -y
RUN  yum install python -y
COPY ./components/get-pip.py /tmp/
RUN python /tmp/get-pip.py
RUN pip install django
RUN pip install gunicorn
WORKDIR /opt/app
EXPOSE 8080
ENTRYPOINT ["gunicorn","-b","0.0.0.0:8080"]


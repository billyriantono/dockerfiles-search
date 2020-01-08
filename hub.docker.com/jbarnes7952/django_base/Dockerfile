FROM jbarnes7952/alpine_base:latest

MAINTAINER john barnes <jbarnes7952@gmail.com>
LABEL Name=django_base
LABEL Version=0.0.1

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="https://github.com/jbarnes7952/django_base.git" \
      org.label-schema.vcs-ref=$VCS_REF

RUN mkdir /app
WORKDIR /app
COPY requirements.txt /app

# make some useful symlinks that are expected to exist
RUN cd /usr/local/bin \
	&& ln -s idle3 idle \
	&& ln -s pydoc3 pydoc \
	&& ln -s python3 python \
	&& ln -s python3-config python-config

RUN pip3 install -r requirements.txt 
RUN django-admin startproject django_project
WORKDIR /app/django_project
RUN python3 manage.py startapp django_app

HEALTHCHECK --interval=10s --timeout=3s \
  CMD curl -f http://localhost:8000/ || exit 1

ENTRYPOINT ["python3", "manage.py", "runserver"]



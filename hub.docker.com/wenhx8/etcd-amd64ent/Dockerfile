FROM python:3.6

#Create and use workdir
RUN mkdir -p /usr/app
RUN mkdir /static
WORKDIR /usr/app

#Copy sources
COPY ./ ./

#Disable bufferent output in python
ENV PYTHONUNBUFFERED 1

#Install dependencies
RUN pip3 install -r requirements.txt
RUN pip3 install gunicorn

ENV DJANGO_STATIC_ROOT /static
EXPOSE 8000
ENV DJANGO_PORT 8000
#Run django app
CMD ["sh", "./run.sh"]
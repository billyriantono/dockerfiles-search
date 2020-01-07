FROM python:3.5

MAINTAINER kevin.marilleau@gmail.com

WORKDIR /home

ADD https://rawgit.com/daimebag/docker-python/master/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
RUN rm requirements.txt

CMD [ "python" ]

FROM ubuntu
MAINTAINER Renan Palmeira <renan@forleven.com>

ENV DEBIAN_FRONTEND noninteractive
ENV INITRD No

# install packages
RUN apt-get update
RUN apt-get install -y git-core python-psycopg2 python-imaging python-pip

# setup app
RUN mkdir /deploy/
ADD myblog /deploy/myblog
RUN (cd /deploy/myblog && pip install -r requirements.txt)
RUN (cd /deploy/myblog && python manage.py syncdb --noinput)
RUN (cd /deploy/myblog && python manage.py migrate --noinput)
RUN (cd /deploy/myblog && python manage.py collectstatic --noinput)

# clean packages
RUN apt-get clean
RUN rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

# expose mysql port
EXPOSE 8000

CMD (cd /deploy/myblog && /usr/local/bin/honcho start)

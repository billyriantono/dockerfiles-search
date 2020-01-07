FROM python:3.6
ENV PYTHONUNBUFFERED 1

ENV CELERY_BROKER_URL redis://redis:6379/0
ENV CELERY_RESULT_BACKEND redis://redis:6379/0
ENV C_FORCE_ROOT true

# copy source code
RUN mkdir /code
COPY perfserver/ /django-celery
COPY requirements.txt  /django-celery
WORKDIR /django-celery

# install requirements
RUN pip install -r requirements.txt

RUN groupadd -r celery && useradd -r -g celery celery
RUN mkdir /home/celery/
RUN mkdir /home/celery/.ssh
RUN chown celery:celery -R /home/celery/
ADD id_rsa.pub /home/celery/.ssh/id_rsa.pub
ADD id_rsa /home/celery/.ssh/id_rsa
RUN chown celery:celery -R /home/celery/.ssh


USER celery
RUN chmod 400 /home/celery/.ssh/id_rsa

# run the worker
#ENTRYPOINT ['celery']
#CMD ['-A','tasks', 'worker','--loglevel=info']
#ENTRYPOINT celery -A tasks worker --loglevel=info

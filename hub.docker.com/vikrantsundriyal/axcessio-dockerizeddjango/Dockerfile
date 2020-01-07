FROM python:3.4

RUN mkdir django-on-docker && cd django-on-docker \
    && mkdir app && cd app \
    && python -m pip install django \
    && mkdir /django-on-docker/app/axcessiot

WORKDIR /django-on-docker/app/axcessiot 
COPY iot-admin-rest/ /django-on-docker/app/axcessiot/ 
RUN python -m pip  install -r /django-on-docker/app/axcessiot/requirements.txt \
    && cp /django-on-docker/app/axcessiot/simple_history_updates/*  /usr/local/lib/python3.4/site-packages/simple_history/
CMD python /django-on-docker/app/axcessiot/manage.py runserver 0.0.0.0:8000

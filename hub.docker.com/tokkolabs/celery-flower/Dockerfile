FROM python:2.7

ENV PYTHONUNBUFFERED 1
ENV C_FORCE_ROOT "true"

#Install requirements
COPY ./requirements.txt /requirements.txt
RUN pip install -r /requirements.txt

CMD flower --broker=${FLOWER_BROKER} --broker_api=${FLOWER_BROKER_API} --max_workers=${FLOWER_MAX_WORKERS}

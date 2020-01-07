FROM python:2.7
LABEL maintainer "Alexandre Norman <norman@xael.org>"

COPY requirements.txt /requirements.txt
RUN pip install -r requirements.txt
ADD django /django

EXPOSE 389

ENTRYPOINT ["python", "/django/manage.py", "server"]


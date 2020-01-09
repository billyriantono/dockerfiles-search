FROM python:3.7.3-alpine3.10
LABEL maintainer="lakmal <madawalakmal94@gmail.com>"

RUN mkdir -p /opt/app

WORKDIR /opt/app

EXPOSE 3306 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

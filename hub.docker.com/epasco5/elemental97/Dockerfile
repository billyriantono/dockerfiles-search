FROM ubuntu:18.04
RUN apt-get update
RUN apt-get install -y python3
RUN apt-get install -y python3-pip
ARG PORT
ENV SERVER_PORT=${PORT}
ENV PYTHONUNBUFFERED 1
RUN mkdir /code
WORKDIR /code
COPY ./elemental/django-elemental/elemental/requirements.txt requirements.txt 
RUN pip3 install -r requirements.txt
COPY . /code/

COPY ./elemental/django-elemental/elemental elemental 
CMD ["./elemental/django-elemental/elemental/manage.py runserver 0.0.0.0:8000"]
ENTRYPOINT ["python3"]
EXPOSE 8000

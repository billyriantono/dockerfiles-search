FROM python:latest
MAINTAINER Trevahok ( github.com/trevahok)

RUN mkdir /code
WORKDIR /code

RUN pip3 install gunicorn
COPY requirements.txt . 
RUN pip3 install -r requirements.txt

COPY . . 

EXPOSE 8000

RUN python3 manage.py makemigrations
RUN python3 manage.py migrate

ENTRYPOINT [ "gunicorn", "todo_list.wsgi", "-b", "0.0.0.0:8000", "--workers", "3" ]

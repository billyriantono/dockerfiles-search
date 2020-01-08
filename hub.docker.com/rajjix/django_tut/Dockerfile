FROM python

MAINTAINER Asaad Najjar <rajjix.dev.1992@hotmail.com>

ENV PYTHONUNBUFFERED 1

RUN mkdir /core

WORKDIR /core

COPY requirements.txt requirements.txt

RUN pip install -r requirements.txt
RUN apt-get update && apt-get -y install vim && apt-get -y install bash-completion

COPY main main
COPY templates templates
COPY users users
COPY manage.py README.md ./
COPY .bashrc /root/.bashrc


CMD ["python3", "manage.py", "runserver", "0:80"]

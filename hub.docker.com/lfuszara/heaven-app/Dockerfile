FROM python:3
ENV PYTHONUNBUFFERED 1

RUN apt-get update
RUN apt-get install nano python3-dev libmariadb-dev -y

RUN mkdir /code
WORKDIR /code

RUN git clone https://github.com/lfuszara1/Heaven.git /code

RUN pip install -r requirements.txt
RUN cp .env.example .env

EXPOSE 18000

RUN chmod +x server.sh

ENTRYPOINT server.sh

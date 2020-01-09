FROM python:3.6

RUN pip install moto[server]

EXPOSE 5000

ENTRYPOINT ["moto_server"]
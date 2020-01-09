FROM python:3

WORKDIR /wsgidav

EXPOSE 80

VOLUME [ "/data", "/config" ]

RUN apt-get update &&\
    apt-get install gettext-base -y &&\
    pip install wsgidav cheroot lxml

COPY ./wsgidav.yaml.template .

COPY ./startup.sh .

ENTRYPOINT [ "bash", "startup.sh" ]
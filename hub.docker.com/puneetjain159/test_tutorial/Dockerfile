FROM ubuntu:16.04

RUN apt-get update -y && \
    apt-get install -y python-pip python-dev

COPY ./requirements.txt /api/requirements.txt
COPY ./api/api.py /api/api.py 

WORKDIR /api

RUN pip install -r requirements.txt

EXPOSE 5000

RUN ls

ENTRYPOINT [ "python" ]

CMD [ "api.py" ]
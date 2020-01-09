FROM ubuntu:16.04

MAINTAINER Your Name "karantongay@uvic.ca"

RUN apt-get update -y && \
    apt-get install -y python-pip python python3.5 curl git

# We copy just the requirements.txt first to leverage Docker cache
COPY ./requirements.txt /app/requirements.txt

WORKDIR /app

RUN pip install --upgrade pip

RUN pip install -r requirements.txt

COPY . /app

RUN cd python-sqlparser && python setup.py build && python setup.py install

EXPOSE 5000

ENTRYPOINT [ "python" ]

CMD [ "app.py" ]

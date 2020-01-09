FROM python:3.4

ENV PYTHONUNBUFFERED 1

# init
WORKDIR /usr/src/app
RUN mkdir ./config
COPY config/requirements.txt ./config

# setup
RUN pip3 install --upgrade pip
RUN pip install -r ./config/requirements.txt

# prep
COPY . .


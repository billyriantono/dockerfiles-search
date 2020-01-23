FROM ubuntu:latest

RUN apt-get update -y
RUN apt-get install -y build-essential python3.6 python3.6-dev python3.6-venv
RUN apt-get install -y python3-pip python-pip

COPY . /app

WORKDIR /app

RUN pip3 install -r requirements.txt

ENTRYPOINT [ "python3"]

CMD [ "app.py" ]
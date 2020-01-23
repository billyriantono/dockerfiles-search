FROM debian:9

RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install python -y && apt-get install python-pip -y && apt-get install python-virtualenv -y && apt-get install python-dev -y
RUN apt-get install default-libmysqlclient-dev -y

WORKDIR /home
RUN python -m virtualenv env
COPY requirements.txt .
RUN /bin/bash -c "source env/bin/activate && pip install --upgrade pip && pip install -r requirements.txt "
CMD [ "/bin/bash" ]

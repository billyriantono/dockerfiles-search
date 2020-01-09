FROM ubuntu:12.04
MAINTAINER Arun Chandrasekhar
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q curl python-all python-pip wget
ADD ./webapp /opt/webapp/
WORKDIR /opt/webapp
RUN pip install -r requirements.txt
EXPOSE 8000
CMD ["python", "app.py"]

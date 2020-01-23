# Base image
FROM python:3.7

RUN apt-get update -y
RUN apt-get install vim -y

# Create shared directory for config of file routes
RUN mkdir -p /etc/dirmon

# Create directory for FTP sharing
RUN mkdir -p /var/dirmon/logs
RUN mkdir -p /var/dirmon/monitored

WORKDIR /opt/dirmon
ADD requirements.txt /opt/dirmon
RUN pip install -r requirements.txt

ADD file2kafka /opt/dirmon

# Start container
CMD ["python", "/opt/dirmon/main.py"]


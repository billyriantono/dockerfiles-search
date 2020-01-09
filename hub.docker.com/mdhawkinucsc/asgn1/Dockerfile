FROM ubuntu:latest
MAINTAINER Matthew Hawkins mdhawkin@ucsc.edu)
RUN apt-get update -y
RUN apt-get install -y python-pip python-dev build-essential
COPY . /app
WORKDIR /app
EXPOSE 8180
RUN pip install -r requirements.txt
ENTRYPOINT ["python"]
CMD ["app.py"]
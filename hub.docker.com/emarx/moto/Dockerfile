FROM ubuntu:latest
MAINTAINER Elliot Marx "elliot.marx@affirm.com"

RUN apt-get update && apt-get install -y python python-pip
RUN pip install "moto[server]"
ENTRYPOINT ["moto_server"]
CMD ["-p", "8999", "s3bucket_path"]

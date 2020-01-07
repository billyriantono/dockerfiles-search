FROM ubuntu
MAINTAINER "Yousuff"
RUN apt-get update
RUN apt-get install python-dev python-pip -y
WORKDIR /cflask
ADD requirements.txt /cflask
COPY web.py /cflask
RUN pip install -r requirements.txt
EXPOSE 5000
ENTRYPOINT ["python"]
CMD ["web.py"]


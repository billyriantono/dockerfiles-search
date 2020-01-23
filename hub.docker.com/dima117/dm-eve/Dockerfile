FROM python:3.6
MAINTAINER dima117
RUN mkdir -p /usr/src/restapi
WORKDIR /usr/src/restapi
RUN pip install Eve 
ADD evemain.py .
COPY  . /usr/src/restapi
EXPOSE 5000
CMD ["python", "evemain.py"]





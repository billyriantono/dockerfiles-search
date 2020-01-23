FROM alpine
MAINTAINER Akshay Mohite <akksmohite@gmail.com>

#update packages
RUN ["apk", "update"]
RUN apk add python
COPY . /app
WORKDIR /app
CMD ["python","app.py"]

FROM alpine
MAINTAINER Oscar LLorens "oscllweb@gmail.com"
RUN apk update
RUN apk upgrade
RUN apk add python3
RUN mkdir -p /opt/WhiteMarket
COPY . /opt/WhiteMarket/
WORKDIR /opt/WhiteMarket
RUN pip3 install --upgrade pip
RUN pip3 install -r requirements.txt
ENTRYPOINT ["python3", "manage.py", "runserver", "0:8000"]
EXPOSE 8000
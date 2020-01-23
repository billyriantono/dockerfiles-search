FROM alpine:edge

RUN apk add --update --no-cache python3

EXPOSE 5000

COPY . /app
WORKDIR /app

RUN pip3 install -r requirements.txt

#ENTRYPOINT ["python3", "client.py", "http://AirplaneService:5000"]

#EXPOSE 5000
#
#COPY . /app
#WORKDIR /app
#
#RUN pip3 install -r requirements.txt
#
#CMD python3 server.py

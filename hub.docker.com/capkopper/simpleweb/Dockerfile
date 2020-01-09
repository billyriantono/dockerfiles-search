FROM alpine

RUN apk add --update python py-pip

RUN mkdir /app
ADD files/ /app

RUN cd /app && \
    pip install -r requirements.txt


WORKDIR /app
EXPOSE 5000
CMD ["python", "server.py"]

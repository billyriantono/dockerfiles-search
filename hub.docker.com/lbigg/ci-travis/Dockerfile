FROM alpine:3.5
RUN apk add python3 --update --no-cache --purge && mkdir /app
WORKDIR /app
COPY . .
RUN pip3 install -r requirements.txt
CMD ["python3", "test.py"]

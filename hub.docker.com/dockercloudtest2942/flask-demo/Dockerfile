FROM python:2.7
LABEL maintaner="zerocamus你好，zerocamus@gmail.com"
COPY . /app
WORKDIR /app
RUN pip install flask redis
EXPOSE 5000
CMD [ "python", "app.py" ]

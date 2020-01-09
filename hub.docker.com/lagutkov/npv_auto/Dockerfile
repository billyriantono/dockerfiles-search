FROM python:alpine3.7
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
#RUN apk update && apk add git
EXPOSE 5000
CMD python ./index.py

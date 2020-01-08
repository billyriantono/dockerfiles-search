FROM alpine:latest

RUN apk -U --no-cache add py3-flask

WORKDIR /runtime/app

ENV FLASK_APP=app.py

EXPOSE 5000

CMD [ "flask", "run", "--host=0.0.0.0"]

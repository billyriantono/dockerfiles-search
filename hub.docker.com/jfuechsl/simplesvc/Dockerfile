FROM python:3.7-alpine

ADD . /app
WORKDIR /app
RUN pip install -r requirements.txt
ENV FLASK_APP=simplesvc \
    FLASK_ENV=production
EXPOSE 5000
CMD ["flask", "run", "-h", "0.0.0.0"]

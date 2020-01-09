FROM python:3.5
LABEL maintainer comp3916

WORKDIR /app

COPY requirements.txt /app
RUN pip install -r requirements.txt

ADD app /app

EXPOSE 5000

CMD python app.py

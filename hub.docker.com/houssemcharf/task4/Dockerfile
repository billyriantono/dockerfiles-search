FROM python:3.7.1

RUN mkdir /app
WORKDIR /app

COPY . /app/

RUN pip install --upgrade pip && \
    pip install flask

ADD . /app

EXPOSE 8069

CMD flask run -p 8069 --host=0.0.0.0 
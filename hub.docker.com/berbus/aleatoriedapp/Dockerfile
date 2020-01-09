FROM python:3.6.7

RUN mkdir /aleatoriedapp
WORKDIR /aleatoriedapp

COPY ./aleatoriedad /aleatoriedapp/aleatoriedad
COPY ./originalidad /aleatoriedapp/originalidad
COPY ./templates /aleatoriedapp/templates
COPY ./static /aleatoriedapp/static
COPY manage.py /aleatoriedapp/manage.py
COPY requirements.txt /aleatoriedapp/requirements.txt

RUN pip3 install --upgrade pip
RUN pip3 install -r requirements.txt

CMD gunicorn originalidad.wsgi --log-file –

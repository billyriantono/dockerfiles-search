FROM python:3.7
ADD . /usr/src/app
WORKDIR /usr/src/app
COPY requirements.txt ./
RUN pip install -r requirements.txt
EXPOSE 8888
CMD python manage.py migrate
CMD exec gunicorn mobile.wsgi:application --bind 0.0.0.0:8888 --workers 3 --log-level DEBUG
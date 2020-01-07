FROM python:3
ENV PYTHONUNBUFFERED 1
ADD requirements.txt .
RUN pip install -r requirements.txt
COPY application application
ENTRYPOINT cd application; python manage.py makemigrations tcgtools && python manage.py migrate; gunicorn -w 2 -b 0.0.0.0:80 tcgtools.wsgi:application

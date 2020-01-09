FROM python:3

ADD . /usr/src/

RUN apt-get update && apt-get -y install gettext
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

WORKDIR /usr/src/app

EXPOSE 8000

COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]
#CMD python manage.py runserver 0.0.0.0:8000
#CMD [ "python", "./manage.py runserver 0.0.0.0:8000" ]

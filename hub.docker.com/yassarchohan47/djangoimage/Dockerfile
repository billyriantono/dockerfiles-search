FROM python:latest
RUN mkdir /music_service
WORKDIR /music_service
RUN pip install virtualenv
ADD . /music_service/
EXPOSE 9000
RUN virtualenv virtenv
ENV VIRTUAL_ENV /env
ENV PATH /env/bin:$PATH
RUN . virtenv/bin/activate
RUN pip install django
RUN pip install djangorestframework
RUN pip install pytz
RUN pip install pyJWT
RUN pip install gunicorn
CMD bash -c "python manage.py makemigrations && python manage.py migrate && gunicorn -w 1 --bind 0.0.0.0:9000 api.wsgi && python manage.py runserver 9000"
FROM python

RUN pip install django

RUN django-admin startproject app

RUN echo 'alias hey="python manage.py"' >> ~/.bashrc

WORKDIR /app

CMD python manage.py runserver 0:8000

EXPOSE 8000

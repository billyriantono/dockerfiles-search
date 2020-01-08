FROM python:alpine
ENV PYTHONUNBUFFERED 1
RUN mkdir /code
WORKDIR /code
ADD requirements.txt /code/
RUN pip install -r requirements.txt
ADD . /code/
VOLUME /code
CMD python src/core/manage.py runserver 0.0.0.0:8000
EXPOSE 8000:8000

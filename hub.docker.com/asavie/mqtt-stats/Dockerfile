FROM python:3.6

# Ensure that Python outputs everything that's printed inside
# the application rather than buffering it.
ENV PYTHONUNBUFFERED 1

RUN mkdir /kube
RUN mkdir /www
RUN mkdir /www/static

COPY ./kube /kube

EXPOSE 8000

WORKDIR /kube
RUN pip install -r requirements.txt

CMD [ "python", "./manage.py", "runserver", "0.0.0.0:8000" ]

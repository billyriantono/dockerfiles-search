FROM python:alpine3.7

# add file
ADD * /

# install
RUN pip install -r requirements.txt

ENTRYPOINT gunicorn -b0.0.0.0:$FLASK_PORT app:app

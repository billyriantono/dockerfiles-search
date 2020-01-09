FROM python:3.6-alpine
RUN mkdir /code
WORKDIR /code
COPY . .
ENV FLASK_APP app.py
ENV FLASK_RUN_HOST 0.0.0.0
RUN apk update && apk add --no-cache coreutils
RUN apk --no-cache add build-base bash
RUN apk add --no-cache --virtual .build-deps gcc musl-dev openssl-dev libffi-dev linux-headers python3-dev postgresql-dev
RUN pip install pipenv
RUN pipenv install cython
RUN pipenv install --system --deploy
#RUN apk del .build-deps gcc musl-dev openssl-dev libffi-dev
EXPOSE 5000
CMD ["gunicorn", "-b", "0.0.0.0:5000", "app:app"]

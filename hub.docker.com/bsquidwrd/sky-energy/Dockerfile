FROM python:3.6-jessie

RUN mkdir /code/
WORKDIR /code/

ADD requirements.txt /requirements.txt
RUN python -m pip install -U pip
RUN pip install --no-cache-dir -r /requirements.txt

ADD . /code/

ENV CLIENT_ID='0'
ENV TOKEN='0'
ENV OWNER_ID='131224383640436736'

ENV DJANGO_SETTINGS_MODULE='db.settings'
ENV DATABASE_ENGINE='django.db.backends.sqlite3'
ENV DATABASE_HOST='placeholder'
ENV DATABASE_PORT='placeholder'
ENV DATABASE_NAME='guildbot.db'
ENV DATABASE_USERNAME='placeholder'
ENV DATABASE_PASSWORD='placeholder'
ENV DEBUG_MODE='true'
ENV SECRET_KEY='placeholder'

CMD ["python", "/code/bot.py"]

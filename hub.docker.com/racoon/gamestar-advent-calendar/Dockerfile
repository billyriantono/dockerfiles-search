FROM python:3.7-alpine

WORKDIR /gamestar-advent-calendar

# COPY config.ini       /gamestar-advent-calendar
COPY requirements.txt /gamestar-advent-calendar/requirements.txt
COPY submit.py        /gamestar-advent-calendar/submit.py

RUN pip3 install -r requirements.txt

ENTRYPOINT [ "python3", "submit.py" ]

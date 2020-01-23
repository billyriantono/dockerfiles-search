FROM python:3

ADD requirements.txt /

ADD _version.py /

ADD __main__.py /

RUN pip install -r requirements.txt

CMD python __main__.py -H 10.132.0.4 -P 27017 -D db-mongo -u user-mongo -p myPassword01 -A mon_api_bracelet

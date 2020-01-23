FROM python
ADD __main__.py /
ADD _version.py /
ADD requirements.txt /

RUN pip install -r requirements.txt
RUN chmod u+x __main__.py
CMD /__main__.py -H 0.0.0.0 -P 27017 -D ma_database_mongo -u mon_user_mongo -p mon_password_mongo -A mon_api-store-to-db

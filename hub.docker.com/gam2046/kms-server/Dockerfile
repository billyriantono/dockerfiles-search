FROM python:2.7.15-alpine

WORKDIR /home/
EXPOSE 1688

RUN wget https://github.com/myanaloglife/py-kms/archive/master.zip && \
  unzip master.zip

CMD [ "python","/home/py-kms-master/server.py" ]

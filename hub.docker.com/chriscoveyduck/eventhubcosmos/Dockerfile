FROM python:3

WORKDIR /usr/src/app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY cosmos_mongo.py ./
COPY eventdict.py ./
COPY eventhub.py ./
COPY main.py ./

CMD [ "python", "./main.py" ]
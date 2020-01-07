FROM python:3

WORKDIR /usr/src/app
COPY . .
#COPY requirements.txt ./
#COPY sonar-client.py ./
RUN pip install --no-cache-dir -r requirements.txt

CMD [ "python", "./sonar-client.py" ]

FROM python:3.7-slim

COPY . /app
WORKDIR /app

RUN chmod +x entrypoint.sh
RUN pip3 install -r requirements.txt


#ENTRYPOINT ["python3","minimal.py","runserver","0.0.0.0:8000"]
ENTRYPOINT ["sh","entrypoint.sh"]

FROM mysql:5.5

EXPOSE 3306

RUN apt-get update && apt-get install -y python3 && apt install -y python3-pip

WORKDIR /app
COPY . /app
RUN chmod 777 /app/start.sh

RUN pip3 install -r requirements.txt

#CMD ["python3", "database.py", "flights.txt>0"]

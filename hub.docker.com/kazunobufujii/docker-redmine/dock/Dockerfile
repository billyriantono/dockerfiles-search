FROM ubuntu:latest
RUN apt-get update -y
RUN apt install python -y
RUN apt install python-pip -y 
COPY . /app
WORKDIR /app
RUN python -m pip install -r requirements.txt
CMD ["python","-m","flask","run","--host=0.0.0.0"]

FROM python:2.7

WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

RUN apt-get update \
	&&apt-get install nano

# Instalacion de las dependencias
RUN pip install -r requirements.txt

#ENTRYPOINT ["python", "xsschallenge.py"]


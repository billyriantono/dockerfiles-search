FROM python:3-alpine
MAINTAINER Jose Viñas <jmvinasr@correo.ugr.es>
WORKDIR proyectoTPV/
COPY /src requirements.txt API_WEB.py /tests ./
COPY data  ./data
RUN pip install --no-cache-dir -r requirements.txt
EXPOSE 80
CMD gunicorn API_WEB:app --log-file=- --bind 0.0.0.0:80

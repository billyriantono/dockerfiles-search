# Basavspegling
FROM alpine:latest

# Installera python och pip
RUN apk add --update py-pip

# Uppgradera pip
RUN pip install --upgrade pip

# Installera Pythonmoduler
COPY requirements.txt /usr/src/app/
RUN pip install --no-cache-dir -r /usr/src/app/requirements.txt

# Kopiera filer
COPY app.py /usr/src/app/
COPY templates/index.html /usr/src/app/templates/

# Exponering av port f app
EXPOSE 5000

# Starta app
CMD ["python", "/usr/src/app/app.py"]


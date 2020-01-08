# base image
FROM alpine:latest

# install python pip package and all its dependencies
RUN apk add --update py2-pip

# install all requirements for our application
COPY requirements.txt /usr/src/app/
RUN pip install --no-cache-dir -r /usr/src/app/requirements.txt

# install our files
COPY app.py /usr/src/app/
COPY templates/index.html /usr/src/app/templates/

# port exposed
EXPOSE 5000

# run the application
CMD ["python", "/usr/src/app/app.py"]

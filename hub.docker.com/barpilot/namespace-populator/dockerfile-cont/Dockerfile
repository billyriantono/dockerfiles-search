#Dockerfile
FROM python:3

WORKDIR /usr/src/app
RUN pip install --no-cache-dir pandevice requests

#Creat new user to avoid permission issues if script produces a file.
RUN useradd -ms /bin/bash panUser
USER panUser

CMD [ "python", "$SCRIPT" ]

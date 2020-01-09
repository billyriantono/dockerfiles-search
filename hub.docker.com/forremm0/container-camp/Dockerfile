FROM alpine

# install python and pip
RUN apk add --update py3-pip

# copy the application file to the image
COPY app.py /usr/src/app/

# tell docker what to run by default
CMD python3 /usr/src/app/app.py

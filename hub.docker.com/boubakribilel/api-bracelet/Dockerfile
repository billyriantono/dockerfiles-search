FROM python:3
ADD __main__.py /app
ADD requirements.txt /app
ADD _version.py /app
WORKDIR /app
RUN pip install -r requirements.txt
CMD [ "python", "/app/__main__.py" ]

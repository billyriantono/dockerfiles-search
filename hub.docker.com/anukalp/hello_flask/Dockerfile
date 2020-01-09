FROM anukalp/python3image:1

RUN pip install flask

RUN mkdir /hello_flask

COPY . /hello_flask

CMD cd /hello_flask && python hello_flask.py

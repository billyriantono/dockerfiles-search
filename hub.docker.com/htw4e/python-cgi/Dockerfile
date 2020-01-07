FROM python:3.7
RUN mkdir /app
ADD . /app
WORKDIR /app
RUN chmod -R 0755 cgi-bin/
RUN pip install -r requirements.txt
CMD python -m http.server --cgi 8000

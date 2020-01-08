FROM python

COPY flask-server.py .
COPY run-server .
COPY test_selector.html .
COPY requirements.txt .

RUN pip install -r requirements.txt
RUN chmod +x run-server

EXPOSE 80

CMD ./run-server



#flaviomeira10 / python-services
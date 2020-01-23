FROM python:3.6
EXPOSE 5003
WORKDIR /app
COPY requirements.txt /app
COPY templates /app/templates
RUN pip install -r requirements.txt
COPY app.py /app
CMD python3.6 app.py


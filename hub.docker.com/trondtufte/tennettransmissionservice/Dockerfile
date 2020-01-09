FROM python:3.7
COPY src /app
COPY requirements.txt /app
WORKDIR /app
RUN pip install --upgrade pip
RUN pip install -r requirements.txt
WORKDIR /app
EXPOSE 5000
CMD ["gunicorn", "-w", "1", "-b", "0.0.0.0:5000","app:app"]
#CMD [ "python", "app.py" ]

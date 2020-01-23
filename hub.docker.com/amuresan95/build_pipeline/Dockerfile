FROM python:3
ADD . /code
WORKDIR /code
RUN pip install -r requirements.txt
RUN chmod +x app.py
CMD ["python3", "app.py"]

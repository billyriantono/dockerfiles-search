FROM tensorflow/tensorflow:1.12.0

RUN pip install --no-cache-dir flask==1.0.2 tensorflow-serving-api==1.12.0

COPY app.py /webapp/app.py
COPY static /webapp/static
COPY templates /webapp/templates

CMD ["python", "/webapp/app.py"]

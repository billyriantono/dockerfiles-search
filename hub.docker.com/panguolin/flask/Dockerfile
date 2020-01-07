FROM python:alpine 

RUN pip install flask

COPY web /web/

EXPOSE 5000

ENTRYPOINT ["python", "/web/app.py"]

FROM python:3.6-stretch
WORKDIR /app
ADD . /app
EXPOSE 80
RUN pip install -r requirements.txt
CMD ["python", "api.py"]
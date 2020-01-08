FROM python:3.7-alpine

RUN pip install --upgrade pip
RUN pip install django
RUN mkdir /app
COPY ./MyProject /app/MyProject
WORKDIR /app/MyProject

EXPOSE 8000/tcp
EXPOSE 8001/tcp
EXPOSE 8002/tcp
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

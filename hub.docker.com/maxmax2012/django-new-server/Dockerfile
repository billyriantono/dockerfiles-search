FROM python:3

WORKDIR /usr/src/app

COPY . .
RUN pip install --no-cache-dir -r requirements.txt
RUN ls
RUN pwd
EXPOSE 8000
WORKDIR /usr/src/app/newserver
CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]

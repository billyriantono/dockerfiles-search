FROM python:3-slim

ENV PYTHONUNBUFFERED 1

RUN echo "django" >> requirements.txt
RUN pip install --upgrade pip && pip install --no-cache-dir -r requirements.txt

WORKDIR /app

RUN django-admin startproject mysite

CMD ["mysite/manage.py","runserver","0:8000"]
ENTRYPOINT ["python"]

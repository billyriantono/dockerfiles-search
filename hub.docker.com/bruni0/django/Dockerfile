FROM python:3.7.2-alpine3.9

COPY Requeriments.txt requirements.txt

RUN pip install -r requirements.txt

COPY . frelance

RUN ls -lha

ENTRYPOINT ["sh", "-c", "python3 frelance/manage.py makemigrations", "python3 frelance/manage.py migrate --no-input", "python3 frelance/manage.py" ,"python3 frelance/manage.py runserver 0.0.0.0:8000" ]
FROM python:3

WORKDIR /usr/src/app

RUN pip install flask flask_sqlalchemy datetime itsdangerous flask_login flask_bcrypt flask_mail pillow flask_wtf wtforms

COPY . .

CMD [ "python", "run.py" ]

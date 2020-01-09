FROM python:3
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
copy requirements.txt /usr/src/app
run pip install -r requirements.txt
copy . /usr/src/app


CMD [ "python", "./Main.py" ]



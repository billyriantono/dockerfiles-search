FROM python:3

WORKDIR /usr/src/app

COPY . .

RUN pip install pipenv
RUN pipenv install --system --deploy  --ignore-pipfile

CMD [ "python", "-m", "srs_notifier" ]

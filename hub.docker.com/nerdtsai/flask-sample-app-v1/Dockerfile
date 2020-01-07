FROM python:3-alpine

RUN pip install pipenv

COPY . /src

WORKDIR /src

# Creates a venv and install packages inside
# RUN pipenv sync

# Installs packages directly in parent. Fails if pipfile.lock out of date
RUN pipenv install --deploy --system

EXPOSE 5000

# To run after pipenv sync
# CMD ["pipenv","run","python","app.py"]

# TO run after system deploy
CMD ["python","/src/app.py"]

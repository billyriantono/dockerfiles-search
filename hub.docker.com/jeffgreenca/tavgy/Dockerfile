FROM python:alpine
LABEL maintainer="jeff.green.ca@gmail.com"
WORKDIR /usr/src/tavgy
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt
RUN pip install pytest pytest-cov
COPY ./src/setup-nltk.py ./setup-nltk.py
RUN [ "python", "setup-nltk.py" ]
COPY ./src/ ./
#CMD [ "python", "game.py", "-v" ]
CMD [ "python", "game.py" ]

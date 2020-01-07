FROM victorbalssa/tflearn-nltk:latest
MAINTAINER victorbalssa <balssa_v@etna-alternance.net>

ADD ./requirements.txt /bot/requirements.txt
WORKDIR /bot
RUN pip install --no-cache-dir -r requirements.txt
EXPOSE 5000

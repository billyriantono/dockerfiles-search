FROM alpine
WORKDIR /usr/src/app
RUN apk update 
RUN apk add nodejs-current
RUN apk add nodejs-npm
RUN npm install pm2
RUN apk --update add tor runit tini
RUN apk add py-pip
RUN pip install virtualenv 
COPY requirements.txt requirements.txt
RUN virtualenv .env
COPY py-googletrans-stable py-googletrans-stable
RUN .env/bin/pip install -r requirements.txt
RUN .env/bin/pip install -e py-googletrans-stable
COPY service service
RUN chmod +x service/tor/run
COPY torrc /etc/tor/torrc
COPY words_dictionary.json .
COPY top10000_words_dictionary.json .
COPY top100000_words_dictionary.json .
COPY words_breaks_by_alphabet words_breaks_by_alphabet
COPY synonym_words.json .
COPY crawler.py .
COPY flask_webservice.py .
COPY backup_frequency.py .
COPY dropbox_backup.py .
COPY process.yaml .
COPY run-services.sh .
RUN mkdir persistence-data
CMD node_modules/pm2/bin/pm2 start process.yaml --no-daemon --log-date-format 'DD-MM HH:mm:ss.SSS'

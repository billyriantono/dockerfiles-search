FROM alpine
RUN apk add bash curl httpie

ADD https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh /wait-for-it
RUN chmod +x /wait-for-it
RUN mv /wait-for-it /bin


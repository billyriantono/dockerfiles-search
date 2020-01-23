FROM python:alpine
WORKDIR /electron
RUN apk --update --no-cache add nodejs
RUN npm install -g electron && npm install electron
CMD ["electron", "."]

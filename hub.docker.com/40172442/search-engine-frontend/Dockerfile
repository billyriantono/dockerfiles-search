FROM nginx:1.11-alpine
COPY . /usr/share/nginx/html

# pull properties from github:
ARG PROVIDER=gcp
ENV PROVIDER ${PROVIDER}
RUN apk --no-cache add curl


RUN curl -O https://raw.githubusercontent.com/nfawcett/searchengine-props/master/$PROVIDER.json
RUN mv *.json /usr/share/nginx/html/config.json

# run command:
#  docker run -d -p 80:80 static
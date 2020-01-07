FROM kmlvision/docker-compose
LABEL MAINTAINER="KML VISION, devops@kmlvision.com"

RUN apk --update --no-cache add git openssh nodejs npm curl && \
    rm -rf /var/lib/apt/lists/*
    
# we require node-gyp installed for installing sqlite3 via npm
RUN npm install -g node-gyp

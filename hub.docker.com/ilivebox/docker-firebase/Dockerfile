FROM node:8-alpine

ARG FIREBASE_TOOLS_VERSION=6.8.0
ENV FIREBASE_TOOLS_VERSION=${FIREBASE_TOOLS_VERSION}

RUN npm install -g firebase-tools@${FIREBASE_TOOLS_VERSION}
RUN npm install -g @google-cloud/functions-emulator

ENV HOST 0.0.0.0

EXPOSE 5000
EXPOSE 9005

WORKDIR /app

CMD ["/bin/sh"]

# FROM cypress/included:3.2.0
# FROM cypress/browsers:chrome67
# FROM cypress/base:8
# FROM whispir/lerna-cypress:latest
FROM cypress/base:10

WORKDIR /cypress_iux
 
COPY package.json .
COPY package-lock.json .
COPY cypress.json .
COPY cypress.env.json .
COPY ["./cypress/integration", "./cypress/integration"]
COPY ["./cypress/plugins", "./cypress/plugins"]
COPY ["./cypress/support", "./cypress/support"]
COPY ["./cypress/config", "./cypress/config"]

RUN npm install
CMD npm run test:$TARGET_ENVIRONMENT
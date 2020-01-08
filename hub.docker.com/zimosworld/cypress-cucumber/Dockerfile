# Docker file for building a container with Cypress
FROM cypress/included:3.4.1
MAINTAINER Jonathan Zimros <john@zimosworld.com>

# Install cypress cucmber preprocessor
RUN npm install cypress-cucumber-preprocessor

ENTRYPOINT ["cypress", "run", "--browser", "chrome"]
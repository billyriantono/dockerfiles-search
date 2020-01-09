FROM cypress/included:3.4.1

RUN apt-get -q update && apt-get -qy install netcat
RUN npm install whatwg-fetch --save-dev
ENTRYPOINT ["cypress", "run"]

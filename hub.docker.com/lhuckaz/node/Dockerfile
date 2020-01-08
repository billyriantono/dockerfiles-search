FROM node:4.5.0

VOLUME ["/usr/src/app"]

RUN echo "#!/bin/bash\n" > /start.sh
RUN echo "npm install" >> /start.sh
RUN echo "npm start" >> /start.sh

RUN chmod +x /start.sh

WORKDIR /usr/src/app

ENTRYPOINT /start.sh
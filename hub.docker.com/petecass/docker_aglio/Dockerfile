FROM node:9

RUN apt-get update -y && apt-get install openssh-client ruby -y
RUN apt-get update -y && apt-get install gconf-service libasound2 libatk1.0-0 \
    libcups2 libdbus-1-3 libgconf-2-4 libgtk-3-0 libnspr4 libx11-xcb1 \
    libxcomposite1 libxcursor1 libxdamage1 libxfixes3 libxi6 libxrandr2 \
    libxss1 libxtst6 libappindicator1 libnss3 lsb-release -y

CMD ["/bin/bash"]

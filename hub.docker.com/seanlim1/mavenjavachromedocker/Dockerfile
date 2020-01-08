from maven:3.5.2-jdk-8

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' >> /etc/apt/sources.list.d/google.list
RUN cat /etc/apt/sources.list.d/google.list

RUN apt-get update && \
    apt-get install -y google-chrome-stable=67.0.3396.99-1

CMD ["echo" "Hello maven 3.5.2 & jdk 8"]

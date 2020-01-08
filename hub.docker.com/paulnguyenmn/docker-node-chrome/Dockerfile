FROM node:latest

# Install Chrome
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list \
  && apt-get update -yqqq \
  && apt-get install -y google-chrome-stable > /dev/null 2>&1

CMD ["node"]

FROM ubuntu:18.04
RUN apt-get update && apt-get -y install chromium-browser
CMD ["chromium-browser", "--headless", "--disable-gpu", "--no-sandbox", "--remote-debugging-port=9222"]

FROM purplelabs/rails

RUN apt-get update -qq \
    && apt-get install -y libx11-xcb1 libxcomposite1 libxcursor1 libxdamage1 libxfixes3 libxi6 libxtst6 libnss3 libnss3 libnspr4 libxss1 libxrandr2 libasound2 libatk1.0-0 libatk-bridge2.0-0 libatspi2.0-0 libgtkhex-3-0 libgtk-3-0 \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

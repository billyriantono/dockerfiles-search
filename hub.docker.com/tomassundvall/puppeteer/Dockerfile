FROM node:8.11.3-slim
RUN apt-get update \
    && apt-get install -yq \
        # libraries
        libasound2 \
        libcups2 \
        libgdk-pixbuf2.0-0 \
        libglib2.0-0 \
        libnss3 \
        libpangocairo-1.0-0 \
        libx11-6 \
        libx11-xcb1 \
        libxcomposite1 \
        libxcursor1 \
        libxdamage1 \
        libxext6 \
        libxrandr2 \
        libxss1 \
        libxtst6 \
        # #fonts
        fonts-liberation \
    && apt-get install -yq libgtk-3-0 --ignore-missing \
    && groupadd -g 999 pptruser \
    && useradd -r -u 999 -g pptruser pptruser
USER pptruser
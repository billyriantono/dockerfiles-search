ARG BASE_TAG=base
FROM yutoma/dev:${BASE_TAG}
RUN apt-get update \
    && apt-get install -y --no-install-recommends gdebi \
    && wget -nv -O chrome.deb https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && gdebi --non-interactive chrome.deb \
    && rm chrome.deb \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
CMD ["google-chrome", "--no-sandbox"]

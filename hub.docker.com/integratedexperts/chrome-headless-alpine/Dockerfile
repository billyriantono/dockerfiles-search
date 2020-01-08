FROM alpine

LABEL maintainer="Alex Skrypnyk <alex@integratedexperts.com>"
LABEL description="Headless Chrome with enabled remote debugging using Alpine image"

RUN apk update && apk upgrade && \
    echo @edge http://nl.alpinelinux.org/alpine/edge/community >> /etc/apk/repositories && \
    echo @edge http://nl.alpinelinux.org/alpine/edge/main >> /etc/apk/repositories && \
    apk add --no-cache \
      chromium@edge \
      freetype@edge \
      harfbuzz@edge \
      nss@edge

RUN mkdir -p /app \
    && addgroup -S chrome \
    && adduser -S -g chrome chrome \
    && mkdir -p /home/chrome/Downloads \
    && chown -R chrome:chrome /home/chrome \
    && chown -R chrome:chrome /app

USER chrome

EXPOSE 9222

ENTRYPOINT [ "/usr/bin/chromium-browser" ]

# @see https://github.com/GoogleChrome/chrome-launcher/blob/master/src/flags.ts
CMD [ \
  # Disable various background network services, including extension updating,
  # safe browsing service, upgrade detector, translate, UMA.
  "--disable-background-networking", \
  # Disable installation of default apps on first run.
  "--disable-default-apps", \
  # Disable all chrome extensions entirely.
  "--disable-extensions", \
  # Disable the GPU hardware acceleration.
  "--disable-gpu", \
  # Disable syncing to a Google account.
  "--disable-sync", \
  # Disable built-in Google Translate service.
  "--disable-translate", \
  # Run in headless mode.
  "--headless", \
  # Hide scrollbars on generated images/PDFs.
  "--hide-scrollbars", \
  # Disable reporting to UMA, but allows for collection.
  "--metrics-recording-only", \
  # Mute audio.
  "--mute-audio", \
  # Skip first run wizards.
  "--no-first-run", \
  # Disable sandbox mode. Note that this switch has security implications.
  # @todo: Get this running without it.
  "--no-sandbox", \
  # Use wildcard IP address for remote debugging connections.
  "--remote-debugging-address=0.0.0.0", \
  # Use port 9222 for remote debugging.
  "--remote-debugging-port=9222", \
  # Disable fetching safebrowsing lists.
  "--safebrowsing-disable-auto-update" \
]

FROM debian:stretch-slim

# To run:
# docker run -d -p 9222:9222 --cap-add=SYS_ADMIN austinfox/chromium-headless

RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    --no-install-recommends \
    && curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list \
    && apt-get update && apt-get install -y \
    google-chrome-unstable \
    --no-install-recommends \
    && apt-get purge --auto-remove -y curl gnupg \
    && rm -rf /var/lib/apt/lists/*

# Add chromium as a user
RUN groupadd -r chromium && useradd -r -g chromium -G audio,video chromium \
    && mkdir -p /home/chromium && chown -R chromium:chromium /home/chromium \
		&& chown -R chromium:chromium /opt/google/

# Run chromium non-privileged
USER chromium

# Expose port 9222
EXPOSE 9222

# Autorun chromium headless with no GPU
ENTRYPOINT [ "google-chrome-unstable" ]
CMD [ "--headless", "--disable-gpu", "--remote-debugging-address=0.0.0.0", "--remote-debugging-port=9222" ]

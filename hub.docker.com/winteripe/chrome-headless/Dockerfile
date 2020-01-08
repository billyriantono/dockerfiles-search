FROM debian:stretch-slim
LABEL name="chrome-headless"

# Install deps + add Chrome Stable + purge all the things
RUN apt-get update && apt-get install -y \
apt-transport-https \
ca-certificates \
curl \
gnupg \
--no-install-recommends \
&& curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
&& echo "deb https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list \
&& apt-get update && apt-get install -y \
google-chrome-stable \
fontconfig \
fonts-ipafont-gothic \
fonts-wqy-zenhei \
fonts-thai-tlwg \
fonts-kacst \
fonts-symbola \
fonts-noto \
ttf-freefont \
--no-install-recommends \
&& apt-get purge --auto-remove -y curl gnupg \
&& rm -rf /var/lib/apt/lists/*

# Add Chrome as a user
RUN groupadd -r chrome && useradd -r -g chrome -G audio,video chrome \
&& mkdir -p /home/chrome && chown -R chrome:chrome /home/chrome \
&& mkdir -p /opt/google/chrome && chown -R chrome:chrome /opt/google/chrome

# Add Entrypoint
COPY docker-entrypoint.sh /bin/docker-entrypoint.sh
RUN chmod +x /bin/docker-entrypoint.sh

# Run Chrome non-privileged
USER chrome

# Env
ENV URL "about:blank"
ENV WINDOW_SIZE "1280,1696"
ENV SHM_SIZE "1024m"
ENV LOG_LEVEL 1
ENV USER_AGENT "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36"

# Expose port 9222
EXPOSE 9222

# Entrypoint
ENTRYPOINT [ "docker-entrypoint.sh" ]

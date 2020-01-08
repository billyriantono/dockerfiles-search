# A minimal Docker image with Node and Puppeteer
#

FROM buildkite/puppeteer

# Install Puppeteer under /node_modules so it's available system-wide
ADD package.json package-lock.json index.js /
RUN npm install

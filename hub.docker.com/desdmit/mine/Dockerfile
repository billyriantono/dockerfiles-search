FROM node:6.12.0-alpine

# ! - Activate when implement unit tests - ! Install chromium for headless browser tests
# ENV CHROME_BIN=/usr/bin/chromium-browser
# RUN apk add --no-cache chromium udev ttf-freefont

# copy context files to image
COPY . /home/

# Install npm packages
WORKDIR /home
RUN npm install && npm run build:prod && mv dist /tmp/ && rm * -rf && mv /tmp/dist .

# Build and run project
# RUN mv dist /tmp/ && rm * -rf && mv /tmp/dist .


EXPOSE 8080
CMD ["node", "dist/server"]
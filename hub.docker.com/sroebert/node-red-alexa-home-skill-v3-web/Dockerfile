# see hooks/build and hooks/.config
ARG BASE_IMAGE_PREFIX
FROM ${BASE_IMAGE_PREFIX}node:12.10

# see hooks/post_checkout
ARG ARCH
COPY qemu-${ARCH}-static /usr/bin

# node-red-alexa

ENV NODE_ENV production

WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install --only=production
COPY . .

CMD ["npm", "start"]

EXPOSE 3000

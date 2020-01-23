# Build
FROM arm32v7/node:10 AS build
COPY qemu-arm-static /usr/bin/
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
RUN npm run build

# Run
FROM arm32v7/node:10
COPY qemu-arm-static /usr/bin/
# Don't run as root user
ENV user kube-slack
RUN addgroup --system $user && adduser --system --ingroup $user $user

WORKDIR /app
COPY package.json /app
RUN npm install --production

COPY --from=build /app/build/ /app
COPY config/ /app/config/

RUN chown -R $user:$user /app
USER $user

CMD ["node", "."]

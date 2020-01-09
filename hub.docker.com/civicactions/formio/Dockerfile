FROM node:10.15.0-alpine

# Note, when updating versions remember to update the sha256sums file:
# sha256sum vX.Y.Z.tar.gz > sha256sums
ENV VERSION=v1.40.0

# Versions below based on dev Dockerfile at https://github.com/formio/formio/blob/master/Dockerfile
# "bcrypt" requires python/make/g++, all must be installed in alpine
# (note: using pinned versions to ensure immutable build environment)
RUN apk add --no-cache python=2.7.15-r1 make=4.2.1-r2 g++=6.4.0-r9

WORKDIR /app
COPY custom-environment-variables.json unattended.patch sha256sums /app/
RUN wget "https://github.com/formio/formio/archive/${VERSION}.tar.gz" \
  && sha256sum -c "sha256sums" \
  && tar --strip-components=1 -xzf "${VERSION}.tar.gz" \
  && rm "${VERSION}.tar.gz" \
  # Apply our patch to allow unattended installation
  && patch -p1 < unattended.patch
# Install config file to allow environment config
COPY custom-environment-variables.json /app/config
# Install dependencies
RUN npm ci

CMD [ "node", "main" ]
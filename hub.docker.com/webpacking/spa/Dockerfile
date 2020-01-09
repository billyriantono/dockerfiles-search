# REF:
# • https://blog.codeship.com/build-minimal-docker-container-ruby-apps/
# • https://medium.com/@fredericlemay/trying-out-the-new-hugos-assets-pipeline-with-docker-61340cd3dfd2
# • https://learnk8s.io/blog/smaller-docker-images

# alpine:3.9
# • node: 10.14.2
# • npm: 6.4.1
# node:11.14-alpine
# • node: 11.14.0
# • npm: 6.7.0


# STAGE: Initialize environment -----------------------------------------------
FROM node:11.14-alpine AS alpine
LABEL alpine=3.9
LABEL node=11.14.0
LABEL npm=6.7.0
RUN \
  apk update && \
  apk upgrade && \
  rm -rf /home/node && \
  rm -rf /var/cache/apk/*


# STAGE: Install npm packages -------------------------------------------------
FROM alpine as node
COPY package.json .
RUN npm install --save-dev --no-package-lock
# RUN npm install --save-dev


# STAGE: Install Webpack required packages ------------------------------------
FROM alpine as webpack
RUN \
  # Install phtyon + yamllint
  apk add --update --no-cache python3 && \
  pip3 install --no-cache-dir yamllint && \
  find / -type d -name __pycache__ -exec rm -r {} + && \
  rm -r /usr/lib/python*/ensurepip && \
  rm -r /usr/lib/python*/lib2to3 && \
  rm -r /usr/lib/python*/turtledemo && \
  rm /usr/lib/python*/turtle.py && \
  rm /usr/lib/python*/webbrowser.py && \
  rm /usr/lib/python*/doctest.py && \
  rm /usr/lib/python*/pydoc.py && \
  rm -rf /root/.cache /var/cache /usr/share/terminfo


# STAGE: Prepare --------------------------------------------------------------
FROM webpack as spa
WORKDIR /home
COPY --from=node node_modules node_modules
# COPY --from=node package*.json ./
COPY . .

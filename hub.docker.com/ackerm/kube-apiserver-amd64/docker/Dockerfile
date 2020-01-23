FROM mhart/alpine-node:11
RUN apk add --no-cache bash && mkdir /prendi
COPY . /prendi
WORKDIR /prendi
RUN cd frontend && \
  yarn && \
  yarn build && \
  cp -r build /prendi && \
  cd /prendi/backend && \
  yarn && \
  cd /prendi && \
  rm -rf /prendi/frontend
WORKDIR /prendi/backend
EXPOSE 80
CMD ["yarn", "start"]
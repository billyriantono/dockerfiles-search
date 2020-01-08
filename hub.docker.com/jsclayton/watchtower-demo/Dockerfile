FROM node:12.13-alpine
WORKDIR /app
COPY . .
RUN yarn
CMD ["node", "index.js"]
ENTRYPOINT ["/app/entrypoint-1.sh"]
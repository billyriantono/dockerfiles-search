FROM mhart/alpine-node:base

WORKDIR /src
ADD . .

ENTRYPOINT ["node", "./lambda_runner.js"]
CMD ["{}"]

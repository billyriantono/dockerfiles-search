FROM jpambrun/ml-base as builder
WORKDIR /home/theia
ENV NODE_OPTIONS --max-old-space-size=4096 
ADD package.json ./package.json
RUN yarn --cache-folder ./ycache && rm -rf ./ycache
RUN yarn theia build

FROM jpambrun/ml-base
WORKDIR /home/theia
COPY --from=builder /home/theia .
EXPOSE 3000
CMD ["bash", "-c", "yarn theia start /src --hostname=0.0.0.0" ]

# --- i think the reason he used this was because he could ensure that the react app is being built using the same node version
FROM mhart/alpine-node:11 AS builder
WORKDIR /app
COPY . .
# first: make sure you have react-scripts and all other things defined in the package.json 
RUN yarn
# now: build the guy and output him where he needs to go
RUN yarn run build

# NOTE: to be available for external access on ECS, we need to be in a non-sudo port
EXPOSE 3000
FROM mhart/alpine-node
RUN yarn global add serve
WORKDIR /app
COPY --from=builder /app/build .
CMD ["serve", "-p", "3000", "-s", "."]

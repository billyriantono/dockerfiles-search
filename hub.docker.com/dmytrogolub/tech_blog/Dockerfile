FROM alpine/git
COPY . /data
WORKDIR /data

##

FROM klakegg/hugo:0.53
COPY --from=0 /data /data
WORKDIR /data
RUN hugo



FROM nginx:alpine
COPY --from=1 /data/public/ /usr/share/nginx/html/

FROM nginx as downloader

RUN apt-get update && apt-get install -y wget curl jq

RUN wget $(curl -s https://api.github.com/repos/UniversalViewer/universalviewer/releases/latest | jq '.tarball_url' | sed 's/"//g') -O uv.tar.gz
RUN tar -xvf uv.tar.gz

RUN mv $(tar -tf uv.tar.gz | grep dist | head -2 | tail -1) /universalViewer

FROM nginx as server
COPY --from=downloader /universalViewer /usr/share/nginx/html
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
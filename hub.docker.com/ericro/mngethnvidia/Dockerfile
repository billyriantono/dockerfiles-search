from nvidia/cuda:8.0-devel
RUN apt-get update && apt-get install -y --no-install-recommends curl ca-certificates libcurl4-openssl-dev
  
COPY Claymore_v11.9/ claymore/
#COPY start.bash /start.bash

ENTRYPOINT ["/claymore/ethdcrminer64"]

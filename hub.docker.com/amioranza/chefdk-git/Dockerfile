FROM chef/chefdk

LABEL maintainer="amioranza@mdcnet.ninja"
LABEL description="Added git to the original image of chefdk"

RUN apt-get update -y \
 && apt-get install -y git \
 && apt-get clean

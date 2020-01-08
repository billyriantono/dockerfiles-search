ARG IMAGE_FROM=therecipe/qt:linux
FROM $IMAGE_FROM

RUN apt-get update \
    && apt-get install -y \
      software-properties-common \
    && add-apt-repository ppa:git-core/ppa \
    && apt-get update \
    && apt-get install -y \
      git


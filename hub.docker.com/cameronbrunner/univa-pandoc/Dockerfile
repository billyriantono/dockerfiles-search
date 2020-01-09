FROM cameronbrunner/pandoc-docker

# install latex packages
RUN apt-get update -y \
  && apt-get install -y --no-install-recommends \
    wget \
    xzdec \
    lmodern \
  && tlmgr init-usertree \
  && tlmgr install bclogo \
  && tlmgr install titlesec

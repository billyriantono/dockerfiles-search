# Dockerfile for EMU development on openSUSE Tumbleweed.

FROM opensuse/tumbleweed
LABEL maintainer="Peter Simons <simons@cryp.to>"

RUN zypper --non-interactive update     \
 && zypper --non-interactive install -y \
      gcc-c++                           \
      ghostscript                       \
      git                               \
      make                              \
      pandoc                            \
      python                            \
      python3-dateutil                  \
      R                                 \
      rsync                             \
      sqlite3                           \
      tar                               \
      texinfo                           \
      texlive-ae                        \
      texlive-cjk                       \
      texlive-fancyvrb                  \
      texlive-isodate                   \
      texlive-parskip                   \
      texlive-substr                    \
      zlib-devel

RUN Rscript --vanilla -e 'install.packages(c("data.table","xtable","RSQLite","RPostgreSQL","plan"),repos="https://cloud.r-project.org")'

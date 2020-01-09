FROM tianon/latex

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y python-pygments
RUN  apt autoremove && apt autoclean && rm -rf /var/lib/apt/lists/*


# RUN tlmgr update --self && tlmgr update --all
# RUN tlmgr install keyval kvoptions fancyvrb fvextra upquote float ifthen calc ifplatform pdftexcmds etoolbox xstring xcolor lineno framed shellesc
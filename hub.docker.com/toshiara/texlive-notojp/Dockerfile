FROM paperist/alpine-texlive-ja

# Reference: https://hub.docker.com/r/solareenlo/alpine-texlive-ja

ARG FONTURL=https://github.com/googlefonts/noto-cjk/raw/master

RUN apk --no-cache add wget && \
    mkdir -p /usr/local/texlive/texmf-local/fonts/opentype/google && \
    cd /usr/local/texlive/texmf-local/fonts/opentype/google/ && \
    # install only jp fonts of google noto font cjk
    wget ${FONTURL}/NotoSansJP-Black.otf \
         ${FONTURL}/NotoSansJP-Bold.otf \
         ${FONTURL}/NotoSansJP-DemiLight.otf \
         ${FONTURL}/NotoSansJP-Light.otf \
         ${FONTURL}/NotoSansJP-Medium.otf \
         ${FONTURL}/NotoSansJP-Regular.otf \
         ${FONTURL}/NotoSansJP-Thin.otf \
         ${FONTURL}/NotoSerifJP-Black.otf \
         ${FONTURL}/NotoSerifJP-Bold.otf \
         ${FONTURL}/NotoSerifJP-ExtraLight.otf \
         ${FONTURL}/NotoSerifJP-Light.otf \
         ${FONTURL}/NotoSerifJP-Medium.otf \
         ${FONTURL}/NotoSerifJP-Regular.otf \
         ${FONTURL}/NotoSerifJP-SemiBold.otf && \
    mktexlsr && \
    apk --no-cache del wget

RUN apk --no-cache add curl && \
    tlmgr update --self && \
    tlmgr install ccicons newtx siunitx stix

# Mincho, light     (\mcfamily\ltseries)
# Mincho, medium    (\mcfamily\mdseries)
# Mincho, bold      (\mcfamily\bfseries)
# Gothic, medium    (\gtfamily\mdseries)
# Gothic, bold      (\gtfamily\bfseries)
# Gothic, extrabold (\gtfamily\ebseries)
# MaruGothic        (\mgfamily)

# To use above 7 fonts, add below 2 lines in preamble of .tex file
# \usepackage[deluxe]{otf}
# \usepackage[noto-jp]{pxchfon}

WORKDIR /workdir
VOLUME ["/workdir"]
CMD ["sh"]


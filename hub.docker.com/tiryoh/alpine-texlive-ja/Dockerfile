# Copyright (c) 2016 Kaito Udagawa
# Copyright (c) 2016-2019 3846masa
# Copyright (c) 2020 Daisuke Sato
# Released under the MIT license
# https://opensource.org/licenses/MIT

FROM frolvlad/alpine-glibc:latest

ENV PATH /usr/local/texlive/2019/bin/x86_64-linux:$PATH

RUN apk add --no-cache perl fontconfig-dev freetype-dev make ghostscript && \
    apk add --no-cache --virtual .fetch-deps wget xz tar && \
    mkdir /tmp/install-tl-unx && \
    wget -qO - ftp://tug.org/historic/systems/texlive/2019/install-tl-unx.tar.gz | \
    tar -xz -C /tmp/install-tl-unx --strip-components=1 && \
    printf "%s\n" \
      "selected_scheme scheme-basic" \
      "tlpdbopt_install_docfiles 0" \
      "tlpdbopt_install_srcfiles 0" \
      > /tmp/install-tl-unx/texlive.profile && \
    /tmp/install-tl-unx/install-tl \
      --profile=/tmp/install-tl-unx/texlive.profile && \
    tlmgr install \
      collection-latexextra \
      collection-fontsrecommended \
      collection-langjapanese \
      latexmk && \
    rm -fr /tmp/install-tl-unx && \
    apk del .fetch-deps

# References: https://gist.github.com/e10101/a4e833120f8a66a22cd581241cc79ed0
#           : https://qiita.com/zr_tex8r/items/9dfeafecca2d091abd02
#           : https://github.com/googlefonts/noto-cjk
# install noto font jp
# フォントをインストールする場所は以下で探し, /fonts/以下は自由なディレクトリが可能.
# $ kpsewhich -var-value=TEXMFLOCAL
RUN mkdir -p /usr/local/texlive/texmf-local/fonts/opentype/google && \
    cd /usr/local/texlive/texmf-local/fonts/opentype/google/ && \
    # 以下はgoogle noto font cjkのjpフォントだけをインストールしている.
    wget https://github.com/googlefonts/noto-cjk/raw/master/NotoSansJP-Black.otf \
         https://github.com/googlefonts/noto-cjk/raw/master/NotoSansJP-Bold.otf \
         https://github.com/googlefonts/noto-cjk/raw/master/NotoSansJP-DemiLight.otf \
         https://github.com/googlefonts/noto-cjk/raw/master/NotoSansJP-Light.otf \
         https://github.com/googlefonts/noto-cjk/raw/master/NotoSansJP-Medium.otf \
         https://github.com/googlefonts/noto-cjk/raw/master/NotoSansJP-Regular.otf \
         https://github.com/googlefonts/noto-cjk/raw/master/NotoSansJP-Thin.otf \
         https://github.com/googlefonts/noto-cjk/raw/master/NotoSerifJP-Black.otf \
         https://github.com/googlefonts/noto-cjk/raw/master/NotoSerifJP-Bold.otf \
         https://github.com/googlefonts/noto-cjk/raw/master/NotoSerifJP-ExtraLight.otf \
         https://github.com/googlefonts/noto-cjk/raw/master/NotoSerifJP-Light.otf \
         https://github.com/googlefonts/noto-cjk/raw/master/NotoSerifJP-Medium.otf \
         https://github.com/googlefonts/noto-cjk/raw/master/NotoSerifJP-Regular.otf \
         https://github.com/googlefonts/noto-cjk/raw/master/NotoSerifJP-SemiBold.otf && \
    mktexlsr

WORKDIR /workdir

CMD ["sh"]

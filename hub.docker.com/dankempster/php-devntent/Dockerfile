FROM python:2.7

MAINTAINER Daniel Siepmann
LABEL Description="This image is used to ease TYPO3 Documentation rendering with Sphinx." Vendor="DanielSiepmann" Version="1.0"

# Install TYPO3 pip requirements
    RUN pip install Sphinx && \
        pip install pyyaml && \
        pip install Pillow

# Install TYPO3 specific pip packages like theme.
    RUN pip install t3SphinxThemeRtd && \
        pip install t3fieldlisttable && \
        pip install t3tablerows && \
        pip install t3targets

    RUN cd /usr/local/lib/python2.7/site-packages/pygments/lexers/ && \
        wget https://raw.githubusercontent.com/Tuurlijk/Pygments-TypoScript-Lexer/master/typoscript.py && \
        python _mapping.py

    WORKDIR /home/t3-sphinx/_make

    ENTRYPOINT ["make"]

FROM node

# Install
RUN apt-get update && apt-get install -y \
  git

# Install revealjs
RUN mkdir -p /revealjs
WORKDIR /revealjs
RUN git clone https://github.com/hakimel/reveal.js.git . && \
    git checkout tags/3.7.0 -b 3.7.0
RUN npm install

RUN mkdir -p /revealjs/presentations

# Add index html for redirect (dirty fix)
ADD ./index.html /revealjs/index.html

# Add demo presentation to give a usage example
ADD ./demo_presentation /revealjs/demo_presentation


#################
#Install Plugins
#################

# Install MathJax
RUN git clone https://github.com/mathjax/MathJax.git /revealjs/MathJax

# Install Menu
RUN git clone https://github.com/denehyg/reveal.js-menu.git /revealjs/plugin/menu


# Install Chalkboard
RUN mkdir -p /revealjs/plugin/chalkboard
RUN git clone https://github.com/rajgoel/reveal.js-plugins.git /revealjs/plugin/tmp && mv /revealjs/plugin/tmp/chalkboard /revealjs/plugin && rm -r /revealjs/plugin/tmp

# Install Footer
RUN mkdir -p /revealjs/plugin/footer && cd /revealjs/plugin/footer && wget https://raw.githubusercontent.com/e-gor/Reveal.js-Title-Footer/master/plugin/title-footer/title-footer.css && wget https://raw.githubusercontent.com/e-gor/Reveal.js-Title-Footer/master/plugin/title-footer/title-footer.js

# Install Charts
RUN mkdir -p /revealjs/plugin/chartjs && cd /revealjs/plugin/chartjs && wget https://gitlab.com/dvenkatsagar/reveal-chart/raw/master/plugin/chartjs/Chart.min.js && wget https://gitlab.com/dvenkatsagar/reveal-chart/raw/master/plugin/chartjs/charted.js

# Install vis.js
RUN mkdir -p /revealjs/plugin/visjs && git clone https://github.com/almende/vis.git /revealjs/plugin/visjs

# Add image metadata
LABEL org.label-schema.license="https://github.com/hakimel/reveal.js/blob/master/LICENSE" \
    org.label-schema.vendor="Hakim El Hattab, Dockerfile provided by Mark Coggeshall, forked from agiled-de/reveal.js-docker" \
	org.label-schema.name="reveal.js" \
	org.label-schema.description="Docker images of reveal.js with select plugins." \
	org.label-schema.vcs-url=$VCS_URL \
	org.label-schema.vcs-ref=$VCS_REF \
	org.label-schema.build-date=$BUILD_DATE \
	org.label-schema.schema-version="rc1" \
	maintainer="Mark Coggeshall <mark.coggeshall@gmail.com>"

ADD ./docker-entrypoint.sh /
RUN chmod u+x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

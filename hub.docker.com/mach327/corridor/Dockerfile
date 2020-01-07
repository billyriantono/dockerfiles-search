from jekyll/minimal
copy drone.sh /usr/bin/
copy --chown=jekyll ./src/ /srv/jekyll/
RUN chown jekyll:jekyll -R /srv/jekyll
volume /srv/jekyll/_data/corridor/

cmd /usr/bin/drone.sh

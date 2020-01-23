FROM plone:5.2.0
COPY buildout.cfg /plone/instance/site.cfg
RUN gosu plone buildout -c site.cfg

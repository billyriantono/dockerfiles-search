# gotchas/pharo-teapot
#FROM gotchas/pharo-rfb
FROM gotchas/pharo70x64
MAINTAINER Christer Assmundsson

EXPOSE 1701
RUN ./pharo-run get Teapot && rm -fr pharo-local
RUN ./pharo-run get XMLParser && rm -fr pharo-local
RUN ./pharo-run get XMLWriter && rm -fr pharo-local
# RUN ./pharo-run get NeoJSON
#RUN chmod -R g=u Pharo* pharo* .config
RUN echo "Teapot installed"

# Neo-Console (used from Telnet)
RUN ./pharo-run config http://www.smalltalkhub.com/mc/SvenVanCaekenberghe/Neo/main ConfigurationOfNeoConsole --install=stable && rm -fr pharo-local
RUN ./pharo-run eval --save 'NeoConsoleTelnetServer new start'

#RFB
EXPOSE 5902
RUN ./pharo-run config http://www.smalltalkhub.com/mc/PharoExtras/RFB/main ConfigurationOfRFB --install=stable && rm -fr pharo-local
# RUN rm -fr pharo-local

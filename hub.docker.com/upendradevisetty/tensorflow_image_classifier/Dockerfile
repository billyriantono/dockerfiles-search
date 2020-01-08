FROM johnfonner/image_classifier:0.1

COPY classify_image.py final.sh /

RUN chmod +x /final.sh

ENTRYPOINT [ "/final.sh" ]

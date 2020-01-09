FROM      alpine:3.7

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

RUN apk update && apk add ocrmypdf \
  unpaper \
  tesseract-ocr-data-fra \
  tesseract-ocr-data-deu \
  tesseract-ocr-data-spa \
  tesseract-ocr-data-por

USER appuser

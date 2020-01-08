FROM golang:1.13

RUN export GO111MODULE=on \
    && go get -u github.com/smartystreets/goconvey \
    && go get github.com/google/wire/cmd/wire@v0.3.0 \
    && go get -u github.com/golangci/golangci-lint/cmd/golangci-lint \
    && go get github.com/99designs/gqlgen@v0.9.3 \
    && go get github.com/vektah/dataloaden@v0.3.0 \
	&& go get -u github.com/rubenv/sql-migrate/sql-migrate
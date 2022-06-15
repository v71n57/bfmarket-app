#build stage
ARG GO_VERSION=1.18
ARG ALP_VERSION=3.16

FROM golang:${GO_VERSION}-alpine${ALP_VERSION} AS builder
WORKDIR /go/src/app
COPY . .
RUN apk add --no-cache git
RUN go get -d -v ./...
RUN go install -v ./...

#final stage
FROM alpine:${ALP_VERSION}
RUN apk --no-cache add ca-certificates
COPY --from=builder /go/bin/app /app
ENTRYPOINT ./app
LABEL Name=ProductService Version=0.0.1
EXPOSE 8082

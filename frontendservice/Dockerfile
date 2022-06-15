#build stage
ARG GO_VERSION=1.18
ARG ALP_VERSION=3.16

FROM golang:${GO_VERSION}-alpine${ALP_VERSION} AS builder
WORKDIR /go/src/app
COPY . .
RUN apk add --no-cache git
RUN go build -o /go/bin/app ./main.go

#final stage
FROM alpine:${ALP_VERSION}
RUN apk --no-cache add ca-certificates
WORKDIR /app
COPY --from=builder /go/bin/app /app
RUN mkdir templates
RUN mkdir static
COPY --from=builder /go/src/app/templates templates/
COPY --from=builder /go/src/app/static static/
ENTRYPOINT ./app
LABEL Name=FrontendService Version=0.0.1
EXPOSE 8082
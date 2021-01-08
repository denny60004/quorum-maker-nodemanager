# Build NodeManager stage
FROM golang:1.15.2-alpine3.12 as build_nodeManager

WORKDIR /app
ENV GO111MODULE=on
RUN apk add --update git make gcc musl-dev linux-headers ca-certificates
COPY . .
RUN go mod download && go build -o /root/quorum-maker/NodeManager main.go

# Build Solc stage
FROM ethereum/solc:0.4.24 as build_solc

# Final stage
FROM alpine:3.12
RUN apk update && apk upgrade && apk add --no-cache --update bash
RUN mkdir -p /root/quorum-maker/NodeManagerUI 
COPY --from=build_nodeManager /root/quorum-maker/NodeManager /tmp
COPY --from=build_solc /usr/bin/solc /usr/local/bin
ADD docker/dist /tmp/NodeManagerUI



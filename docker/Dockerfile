# Build NodeManager stage
FROM golang:1.12 as build_nodeManager

WORKDIR /app
ENV GO111MODULE=on
RUN git clone https://github.com/denny60004/quorum-maker-nodemanager.git && cd quorum-maker-nodemanager && go mod download && go build -o /root/quorum-maker/NodeManager main.go

# Build Solc stage
FROM ethereum/solc:0.4.24 as build_solc

# Final stage
FROM debian:stable-20200908-slim
RUN mkdir -p /root/quorum-maker/NodeManagerUI 
COPY --from=build_nodeManager /root/quorum-maker/NodeManager /root/quorum-maker
COPY --from=build_solc /usr/bin/solc /usr/local/bin
ADD dist /root/quorum-maker/NodeManagerUI


ADD NetworkManagerContract.sol /root/quorum-maker/NetworkManagerContract.sol

FROM ubuntu:18.04

RUN apt-get update
RUN apt-get install -y wget
WORKDIR /tmp
RUN wget https://dl.google.com/go/go1.11.linux-amd64.tar.gz
RUN tar -xvf go1.11.linux-amd64.tar.gz
RUN mv go /usr/local
ENV GOROOT=/usr/local/go
ENV GOPATH=$HOME/go
ENV PATH=$GOPATH/bin:$GOROOT/bin:$PATH
RUN mkdir /mnt/golang
WORKDIR /mnt/golang

VOLUME ["/mnt/golang"]

EXPOSE 80

ENTRYPOINT pwd && ls && go run main.go

#docker run --rm -it -v "$(pwd)"/scripts/:/mnt/golang -p 80:80 gogoland

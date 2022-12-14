FROM golang:1.15

# Define working directory.
WORKDIR /app

ENV CGO_ENABLED=0 GOARCH=amd64 CGO_ENABLED=0 GODEBUG=x509ignoreCN=0

ADD config.yaml  /app/config.yaml
ADD go.mod /app/go.mod
ADD go.sum /app/go.sum
ADD main.go /app/main.go

RUN apt-get update
RUN apt install -y iputils-ping

COPY server.crt /etc/ssl/certs/server.crt 

RUN go clean -modcache && go mod tidy
RUN go mod download
RUN go build -a --installsuffix cgo --ldflags=-s -o pinger

CMD ["go", "run", "main.go"]

EXPOSE 443

FROM golang:1.21 as builder

WORKDIR /app
COPY . .

RUN go mod init example.com/myapp
RUN go get github.com/prometheus/client_golang/prometheus/promhttp
RUN CGO_ENABLED=0 GOOS=linux go build -o myapp

FROM alpine:3.19

WORKDIR /app
COPY --from=builder /app/myapp /app/

EXPOSE 2112
CMD ["/app/myapp"]

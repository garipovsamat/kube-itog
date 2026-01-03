FROM golang:1.21-alpine AS builder
WORKDIR /app
RUN echo 'module kube-itog' > go.mod && \
    echo 'go 1.21' >> go.mod
COPY cmd/info-service/main.go ./cmd/info-service/
RUN CGO_ENABLED=0 GOOS=linux go build -o /info-service ./cmd/info-service/main.go

FROM alpine:latest
WORKDIR /root/
COPY --from=builder /info-service .
ENV INFO_BIND_PORT=8082
EXPOSE 8082
CMD ["./info-service"]
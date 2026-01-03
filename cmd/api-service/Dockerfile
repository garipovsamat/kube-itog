FROM golang:1.21-alpine AS builder

WORKDIR /app

RUN echo 'module kube-itog' > go.mod && \
    echo 'go 1.21' >> go.mod

COPY cmd/api-service/main.go ./cmd/api-service/

RUN CGO_ENABLED=0 GOOS=linux go build -o /api-service ./cmd/api-service/main.go


FROM alpine:latest

WORKDIR /root/

COPY --from=builder /api-service .

ENV API_BIND_PORT=8081

EXPOSE 8081

CMD ["./api-service"]
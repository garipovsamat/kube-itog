FROM golang:1.21-alpine AS builder
WORKDIR /app
RUN echo 'module kube-itog' > go.mod && \
    echo 'go 1.21' >> go.mod
COPY cmd/root-service/main.go ./cmd/root-service/
RUN CGO_ENABLED=0 GOOS=linux go build -o /root-service ./cmd/root-service/main.go

FROM alpine:latest
WORKDIR /root/
COPY --from=builder /root-service .
ENV ROOT_BIND_PORT=8080
EXPOSE 8080
CMD ["./root-service"]
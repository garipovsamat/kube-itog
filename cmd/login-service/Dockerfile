FROM golang:1.21-alpine as builder
WORKDIR /app
RUN echo 'module kube-itog' > go.mod && \
    echo 'go 1.21' >> go.mod
COPY cmd/login-service/main.go ./cmd/login-service/
RUN CGO_ENABLED=0 GOOS=linux go build -o /login-service ./cmd/login-service/main.go

FROM alpine:latest
WORKDIR /root/
COPY --from=builder /login-service .
ENV LOGIN_BIND_PORT=8083
EXPOSE 8083
CMD ["./login-service"]
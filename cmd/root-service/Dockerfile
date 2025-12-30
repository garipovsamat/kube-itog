FROM golang:1.21-alpine as builder
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o /root-service ./cmd/root-service

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /root-service .
ENV ROOT_BIND_PORT=8080
EXPOSE 8080
CMD ["./root-service"]
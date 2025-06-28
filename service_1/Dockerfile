# Build stage
FROM golang:1.21 as builder

WORKDIR /app
COPY . .

RUN go mod download
RUN CGO_ENABLED=0 GOOS=linux go build -o /service1

# Final stage
FROM alpine:latest
RUN apk --no-cache add ca-certificates

WORKDIR /root/
COPY --from=builder /service1 .

EXPOSE 8080
CMD ["./service1"]

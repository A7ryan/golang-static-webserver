# Build stage
FROM golang:1.25-alpine AS builder
WORKDIR /app

COPY go.mod ./
RUN go mod download

COPY . . 
RUN go build -o app .

# Run stage
FROM alpine

RUN adduser -D -u 8877 a7ryan
USER a7ryan

WORKDIR /app

COPY --from=builder /app/app .
COPY --from=builder /app/static /app/static

EXPOSE 8080
CMD ["./app"]

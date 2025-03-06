FROM golang:alpine AS builder
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . /app
RUN CGO_ENABLED=0 GOOS=linux go build -o /app/momo-store ./cmd/api

# Deploy the application binary into a lean image
FROM alpine AS build-release-stage
WORKDIR /app
COPY --from=builder  /app/momo-store ./momo-store
EXPOSE 8081
ENTRYPOINT ["/app/momo-store"]
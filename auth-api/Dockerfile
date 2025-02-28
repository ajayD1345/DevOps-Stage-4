# Stage 1: build the auth-api application
FROM golang:1.21-alphine AS builder
WORKDIR /app

# Install the dependencies first for caching
COPY go.mod go.sum ./
RUN go mod download

# Copy in the source code
COPY . .
# Build the binary; CGO is disabled for a fully static binary
RUN CGO_ENABLED=0 GOOS=linux go build -o auth-api

# Stage 2: create a minimal runtime image
FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/

# Copy the auth-api binary from the building stage
COPY --from=build-builder /app/auth-api .

# Expose the port that the service listens on
EXPOSE 8081

# Start the service
CMD ["./auth-api"]

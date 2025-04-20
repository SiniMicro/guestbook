# Build stage
FROM golang:1.18 AS builder

WORKDIR /app

COPY main.go .

RUN go mod init guestbook
RUN go mod tidy

RUN go build -o main main.go

# Final stage
FROM ubuntu:18.04

# Copy the built binary from the builder stage
COPY --from=builder /app/main /app/guestbook

# Copy static files to the image
COPY public/index.html /app/public/index.html
COPY public/script.js /app/public/script.js
COPY public/style.css /app/public/style.css
COPY public/jquery.min.js /app/public/jquery.min.js

WORKDIR /app

# Expose port 3000
EXPOSE 3000

# Command to run the application
CMD ["./guestbook"]

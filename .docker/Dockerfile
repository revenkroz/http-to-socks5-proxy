FROM golang:1.19.3-alpine AS base

WORKDIR /app

# builder
FROM base AS builder

# build-args
ARG VERSION

RUN apk --no-cache add bash git openssh

# modules: utilize build cache
COPY go.mod ./
COPY go.sum ./

RUN go mod download
COPY . .

ENV CGO_ENABLED=0 GOOS=linux GOARCH=amd64
RUN go build -o app -ldflags "-w -s" .

# runner
FROM scratch AS prod

WORKDIR /app

COPY --from=builder /app/app /app/app
EXPOSE 8080

CMD [ "/app/app" ]

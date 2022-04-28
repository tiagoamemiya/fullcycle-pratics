FROM golang:1.16-alpine AS builder

WORKDIR /app

COPY go.mod ./
RUN go mod download && go mod verify

COPY *.go ./

RUN go build -o ./codeeducation

RUN CGO_ENABLED=0 go build -ldflags="-s -w" -o ./codeeducation

CMD [ "ls -l" ]

FROM scratch

WORKDIR /app

COPY --from=builder /app/codeeducation .

CMD [ "./codeeducation" ]
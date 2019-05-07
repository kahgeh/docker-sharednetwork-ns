FROM golang:alpine as builder
RUN mkdir /build 
ADD . /build/
WORKDIR /build 
RUN go build -o main .

FROM alpine
ARG COMMIT_ID
ENV VERSION "1.0.0"
ENV COMMIT_ID "${COMMIT_ID}"
LABEL VERSION="1.0.0" \ 
    COMMIT_ID=${COMMIT_ID}

COPY --from=builder /build/main /app/
RUN apk add --no-cache curl
WORKDIR /app
CMD ["./main"]
EXPOSE 8081
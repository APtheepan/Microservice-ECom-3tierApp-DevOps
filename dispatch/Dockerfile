FROM golang:1.23 as base
WORKDIR /go/src/app

#COPY go.mod .
#RUN go mod download
COPY *.go .

# install all the dependencies for the project through go init dispatch
RUN go mod init && go get

# build the go code
RUN go build -o main .

# Stage 2
# Use distroless image to reduce the size of the image and increase the security
FROM gcr.io/distroless/base

COPY --from=base /go/src/app/ .

CMD [ "./main" ]

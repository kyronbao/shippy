build:
	GOPROXY=https://goproxy.io GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -a -installsuffix cgo -o consignment-cli .
	docker build -t consignment-cli .

run:
	docker run -e MICRO_REGISTRY=mdns consignment-cli
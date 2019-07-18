build:
	protoc --proto_path=. --micro_out=. --go_out=. proto/vessel/vessel.proto
	GOPROXY=https://goproxy.io GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -a -installsuffix cgo -o  .
	docker build -t consignment-service .
run:
	docker run -p 50051:50051 \
	 -e MICRO_SERVER_ADDRESS=:50051 \
	 -e MICRO_REGISTRY=mdns \
	 consignment-service
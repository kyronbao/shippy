build:
	protoc --proto_path=. --micro_out=. --go_out=. proto/vessel/vessel.proto

	GOPROXY=https://goproxy.io GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -o vessel-service -a -installsuffix \
	  cgo main.go repository.go handler.go datastore.go

	docker build -t vessel-service .
run:
	docker run -p 50051:50051 \
	 -e MICRO_SERVER_ADDRESS=:50051 \
	 -e MICRO_REGISTRY=mdns \
	vessel-service
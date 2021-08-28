## Preview and Planning 
### Postman 
![Output](https://github.com/aritra1999/go_auth/blob/master/request.png)
### POA
![Output](https://github.com/aritra1999/go_auth/blob/master/diagram.png)

## Local Setup 
### Installing and setting up Go in linux (Ubuntu 18.04)
1. Installing Go from the Snap Store: `sudo snap install go`
2. Create Project dir: `mkdir go_auth; cd go_auth`
3. Initialize a Go project: `go mod init go_auth`
4. Install all project dependencies: `go get -d ./...`

### Setting up Redis for token caching
- Install Docker.
- Pull redis container `docker pull redis`
- Run redis container: `sudo docker run -it -p 6379:6379 redis`
- Test conction uing: `redis-cli`
- Connecting Go and Redis: 
	```
	func init() {
	  	//Initializing redis
	  	dsn := os.Getenv("REDIS_DSN")
	  	if len(dsn) == 0 {
	    	dsn = "localhost:6379"
	  	}
  	
	  	client = redis.NewClient(&redis.Options{
	    	Addr: dsn, //redis port
	  	})
	  	_, err := client.Ping().Result()
  	
	  	if err != nil {
	    	panic(err)
	  	}
	}
	```

### Main function and running server
- Main function: 
	```
	func main() {
		router.POST("/login", Login)
		log.Fatal(router.Run(":8080"))
	}
	```
- Start server:  `go run main.go`



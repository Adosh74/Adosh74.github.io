API performance testing is a process of evaluating and measuring the performance and responsiveness of an API under various conditions and loads.

# Load Testing
Load testing for APIs involves simulating high volumes of concurrent requests to test how well the API handles the expected user load.

we can use package like `loadtest` to test the load of our API.

## Install loadtest globally using npm
```bash
npm install -g loadtest
```
or you can install it in your project
```bash
npm install loadtest
```

## Usage of loadtest
### Basic usage

```bash
loadtest -n [number of requests] -c [number of concurrent requests] [url]

# Example
loadtest -n 1000 -c 10 http://localhost:3000/api/v1/users
```

### Options
```bash
-t, --maxSeconds  [number]      Max number of seconds until tests are stopped. Default: 10 seconds
-n, --maxRequests [number]      Number of requests to perform. Default: unlimited in `--maxSeconds` is reached
-c, --concurrency [number]      Number of concurrent requests to perform. Default: 10
-k, --keepAlive                 Use HTTP KeepAlive feature. Default: false
-C, --cookie cookie-name=value  Send a cookie with the given name and value with each request. May be set multiple times.
-H, --header header:value       Send a header with the given name and value with each request. May be set multiple times.
-m, --method [string]           HTTP method to use. Default: GET
```

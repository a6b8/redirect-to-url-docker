Docker Hub: [Pre-Build Image](https://hub.docker.com/r/a6b8/redirect-to-https-docker/)

# Redirect to Url
Redirect all Requests to a given Url

***The Docker Image use Port:*** 80

## Features
- [x] Redirect Request
- [x] Nginx
- [x] Docker
- [x] Docker-Compose
- [x] HA-Proxy Ready
- [x] Rancher (Cattle) Ready

## Quickstart
Docker
```
docker run a6b8/https-redirect-docker
```

Docker-Compose
```
version: '2'
services:
  redirect-to-https:
    image: a6b8/redirect-to-https-docker
```













# docker-nginx-redirect

A very simple container to redirect HTTP traffic to another server, based on `nginx`

## Resources

- [Docker Hub](https://hub.docker.com/r/schmunk42/nginx-redirect/)

## Configuration

### Environment variables

- `SERVER_REDIRECT` - server to redirect to, eg. `www.example.com`
- `SERVER_NAME` - optionally define the server name to listen on eg. `~^www.(?<subdomain>.+).example.com`
   - useful for capturing variable to use in server_redirect. 
- `SERVER_REDIRECT_PATH` - optionally define path to redirect all requests eg. `/landingpage`
   - if not set nginx var `$request_uri` is used
- `SERVER_REDIRECT_SCHEME` - optionally define scheme to redirect to 
   - if not set nginx var `$scheme` is used
- `SERVER_REDIRECT_CODE` - optionally define the http status code to use for redirection
   - if not set or not in list of allowed codes 301 is used as default
   - allowed Codes are: 301, 302, 303, 307, 308
 - `SERVER_REDIRECT_POST_CODE` - optionally define the http code to use for POST redirection
    - useful if client should not change the request method from POST to GET
    - if not set or not in allowed Codes `SERVER_REDIRECT_CODE` is used
    - so per default all requests will be redirected with the same status code
- `SERVER_ACCESS_LOG` - optionally define the location where nginx will write its access log
   - if not set /dev/stdout is used
- `SERVER_ERROR_LOG` - optionally define the location where nginx will write its error log
   - if not set /dev/stderr is used

See also `docker-compose.yml` file.

## Usage

With `docker-compose`

    docker-compose up -d
    
With `docker`    

    docker run -e SERVER_REDIRECT=www.example.com -p 8888:80 schmunk42/nginx-redirect
    docker run -e SERVER_REDIRECT=www.example.com -e SERVER_REDIRECT_PATH=/landingpage -p 8888:80 schmunk42/nginx-redirect
    docker run -e SERVER_REDIRECT=www.example.com -e SERVER_REDIRECT_PATH=/landingpage -e SERVER_REDIRECT_SCHEME=https -p 8888:80 schmunk42/nginx-redirect

---

Built by [dmstr](http://diemeisterei.de)

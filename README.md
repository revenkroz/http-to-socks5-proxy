# HTTP to SOCKS tiny proxy server

The idea is to have a proxy server that can be used to tunnel HTTP traffic to some server through a proxy (e.g. socks5 or http proxy). 
This is useful when you want to use a reverse proxy service to route traffic to a specific host without changing the client code (except base url).

## Usage

__Note:__ For all examples below we assume that the proxy server is socks5 proxy and the target server is https://api.example.com with authentication.

### Executable usage

Add environment variables:
```bash
PROXY_DSN='socks5://test1:test2@123.123.123.123:25000'
TARGET_HOST=https://api.example.com
DEFAULT_HEADERS='Authorization: Bearer test'
IGNORE_SSL=true
```

Run.
```bash
./app
```

### Docker compose usage

```yaml
version: '3.9'

services:
  api_example_com_proxy:
    image: ghcr.io/revenkroz/http-to-socks5-proxy:main
    container_name: proxy
    environment:
      PROXY_DSN: 'socks5://test1:test2@123.123.123.123:25000'
      TARGET_HOST: https://api.example.com
      DEFAULT_HEADERS: 'Authorization: Bearer test'
      IGNORE_SSL: true
    ports:
        - "8080:8080"
```

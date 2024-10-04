# Nick's Homelab - Go Playground

## Description

Golang sandbox in a web application.

## URL

<https://go-playground.nickfedor.dev>

## Original Source Code

<https://go.googlesource.com/playground>
<https://github.com/golang/playground>

## Image Source Repository

<https://github.com/x1unix/go-playground>

## Image Source

<https://hub.docker.com/r/x1unix/go-playground>

## Source Image Setup Documentation

<https://github.com/x1unix/go-playground/tree/master/docs/deployment/docker>

## Integrations

### Traefik

- Using Traefik as a forward proxy to apply a SSL cert to the webpage.

### Authentik

- Traefik middleware is used to enable Authentik to be used for forward auth.

## Notes

- There are no volumes passed to this app, as it's unnecessary.

- The environment variables for the URLs are required to ensure the app
  functions properly.

- As of the current image version (2.1) and Go version (1.23), there are many
  examples that are not working and will return a "405 Method Not Allowed"
  error. As I don't use this service for the examples, it's not an issue, but
  something to just be aware of.

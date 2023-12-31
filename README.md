# Caddy proxy

This repository is a configurable boilerplate to use a Caddy with Let's Encrypt for all your referenced domains as a reverse proxy for your whole infrastructure. Besides that, the github actions in this repository will enable the possibility to manage your Caddy completly with git. So if you want to add or remove a configuration, you can just change the configuration in this repo and github actions will take care of the rest.

## Requirements

There are a few requirements to be able to work with this repository. You need some basic configuration on your server and for your github repository.

### Server
- A public server with root access
- Docker (with access to a registry containing Caddy or already pulled Caddy)
- Shell access with a dedicated user for the github actions with permissions to use docker
- Public key authentication for the user with shell access
- Private key of the user with shell access
- User with shell access should be in group "docker"
- Public available SSH port (Doesn't necessarily have to be 22)
- Ideally port 80 (HTTP) and 443 (HTTPS) open to public - Espc. 80 is necessary for Let's Encrypt to work
- Please make sure that the "caddy" container will automatically startup after reboot

### Github repository
- Configuration like mentioned in the "Setup" section of this README
- Some minutes left for your github actions

## Setup

### Secrets
Create and configurate the following secrets in your github repository.
1. USER - Name of the user with SSH access
2. HOST - Hostname or IP of the server
3. PORT - SSH Port on the server (needs to be open to public in your firewall)
4. PRIVATE_KEY - Private key of the user who should manage the Caddy container on the server

## Workflow

Just modify the Caddyfile to your needs, after your setup. After each Github push, the action will run and the Caddyfile will be validated and deployed to the server.

The workflow is designed to have as few downtimes as possible.

## Known issues

- Host key verification is not used. Please consider to configure a ssh-keyscan based solution in your Github Action configuration.
- "Full (strict)" encryption must be enabled when using Cloudflare.
- Getting Let's Encrypt certifications for public IP adresses isn't possible.

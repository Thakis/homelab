# Installation of Firefly III using Portainer

## Overview
Portainer is a well known container management tool for Docker. It can help you manage your containers, networks and volumes.

You can add Firefly III and the Data Importer as a "stack" using the instructions below.

## Preparation

### Required Configuration Files
You will need to download and save the following configuration files:
- [Docker compose file](https://raw.githubusercontent.com/firefly-iii/docker/main/docker-compose-importer.yml)
- [`stack.env` file with all the environment variables (save as `stack.env`)](https://support.firefly-iii.org/composed.php)

### Edit docker compose file
Open the docker compose file in your favorite editor, and change all references under `env_file:` to say `env_file: stack.env`.

> **Tip**: All `env_file:` references must be pointing to exactly `stack.env`. Nothing else.

### Edit stack.env
You must make the following changes:
1. Change `DB_PASSWORD` in `stack.env` to something else. Pick a nice password.
2. Change `MYSQL_PASSWORD` in `stack.env` to the SAME value (it's at the bottom)
3. Change `FIREFLY_III_URL` in `stack.env` to `http://app:8080`
4. Change `VANITY_URL` in `stack.env` to `http://localhost`

## Installation

### Add docker compose file
1. Open Portainer and go to the environment where you want to install Firefly III (usually the "local" one)
2. Select "Stacks" in the left-hand menu
3. Click "Add stack"
4. Give your stack the name `firefly-iii`
5. Copy-paste the content of your edited docker compose file

### Add stack.env file
1. Upload the `stack.env` file
2. Portainer will expand all the environment variables in the file
3. If you did not make the changes indicated earlier, now is the time

### Deploy
Press the button to get the stack deployed! After a while, it should run as expected.

## Accessing Firefly III
The default configuration will run Firefly III on port 80 which means you can visit Firefly III at `http://localhost`. If your portainer is running somewhere else, or in a different configuration, the URL will be different of course.

---
Source: [Firefly III Documentation](https://docs.firefly-iii.org/how-to/firefly-iii/installation/portainer/)
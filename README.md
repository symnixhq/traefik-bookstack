<br />
<p align="center">
  This repository contains a fully usable <a href="https://github.com/BookStackApp/BookStack"><b>BookStack</b></a> with <a href="https://github.com/traefik/traefik"><b>Traefik</b></a> as a reverse proxy. Additionally, Traefik uses <a href="https://letsencrypt.org/"><b>Let's Encrypt</b></a> as an ACME provider to automate certificate generation.
</p>
<br />

## ⚡️ Installation

1. Make sure you've installed Docker including `docker compose` support on your target system.
   You can install `docker compose` following this instruction: https://docs.docker.com/compose/install/

<br>

2. Clone this repository:

   ```bash
   sudo git clone https://github.com/symnixhq/traefik-bookstack.git
   ```

<br>

3. Open the file called `traefik-letsencrypt-bookstack-docker compose.yml`

<br>

4. Adjust the variables for your configuration. Edit the following values:
   1. Passwords (declared as "MODIFY_ME")
   2. E-Mail address (declared as "example.mail@examplemailservice.com")
   3. Domain (declared as "example.url.com")
   4. PGID and PUID of the user who owns the database data directory

   Edit and Encode the password you want to use in the .env file
   5. It is declared as "${BASICAUTH_PASSWORD}" but needs to be changed in the .env file

Note: You can hash your password with the following line, assuming you installed `htpasswd`before.

```bash
echo $(htpasswd -nb user password) | sed -e s/\\$/\\$\\$/g
```
After you've decrypted your password you need to escape every "$" sign with another "$".

Tip: You can use:

```bash
docker compose convert
```
to resolve your configuration file into the terminal.


<br>

5. Adjust the data volumes

In our example we use:

```yaml
volumes:
  - /data/bookstack/database:/config
```

as the volume that we mount into the container. If you want to use the exact same volumes, you need to create them on your system before. You can do this like this for example:

```bash
sudo mkdir -p /data/bookstack/database
```

<br>

6. Start the project

   ```bash
   sudo docker compose -f <name_of_the_docker_file> up -d
   ```

<br>

7. Check the application logs and verify that everything is running appropriatly

   ```bash
   sudo docker compose logs -f
   ```

<br>

8. Enjoy your new Bookstack installation!

   Note: If you have questions regarding bookstack, have a look at https://www.bookstackapp.com/docs/.

<br>

## 👍 Contribute

See [Contributing](CONTRIBUTING.md).

## ⚠️ License

GPLv3

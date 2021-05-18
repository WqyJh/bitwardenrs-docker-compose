# bitwardenrs-docker-compose

Use docker-compose to deploy bitwardenrs with caddy, having the following features:

- [x] HTTPS
- [x] Let's encrypt certificate apply/renewal

## Usage

1. Clone the repo.

    ```bash
    git clone https://github.com/WqyJh/bitwardenrs-docker-compose bwrs/
    cd bwrs/
    ```

2. Create config files.

    ```bash
    cp .env.template .env
    ```

3. Config domain.

    ```bash
    cat << EOF >> .env
    DOMAIN=https://bitwarden.example.com
    EOF

    cat << EOF > .caddyenv
    DOMAIN=bitwarden.example.com
    EMAIL=bitwarden@example.com
    EOF
    ```

4. Config smtp (optional).

    ```bash
    cat << EOF >> .env
    SMTP_HOST=smtp.
    SMTP_FROM=bitwarden@example.com
    SMTP_FROM_NAME=Bitwarden_RS
    SMTP_PORT=587
    SMTP_SSL=true
    SMTP_EXPLICIT_TLS=true
    SMTP_USERNAME=bitwarden@example.com
    SMTP_PASSWORD=password
    EOF
    ```

5. Start the server.

    ```bash
    docker-compose up -d
    ```

6. Browse https://bitwarden.example.com to register an account and activate it.

7. Then disable signups for security consideration.

    ```bash
    cat << EOF >> .env
    SIGNUPS_ALLOWED=false
    EOF
    docker-compose down
    docker-compose up -d
    ```

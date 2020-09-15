# bitwardenrs-docker-compose

Use docker-compose to deploy bitwardenrs with nginx, having the following features:

- [x] HTTPS
- [ ] Let's encrypt certificate apply/renewal

## Usage

```bash
git clone https://github.com/WqyJh/bitwardenrs-docker-compose
cd bitwardenrs-docker-compose/

cp .env.template .env
```

Config tls certs.

```bash
mkdir -p certs/
cp /path/to/cert.crt certs/
cp /path/to/priv.key certs/
```

Config domain.

```bash
cat << EOF >> .env
DOMAIN=https://bitwarden.example.com
EOF
```

Config smtp (optional).

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

Config nginx.

```bash
sed -i 's/yourhost/bitwarden.example.com/' nginx/conf.d/bwrs.conf
```

Start the server.

```bash
docker-compose up -d
```

Browse https://bitwarden.example.com to register an account and activate it.

Then disable signups for security consideration.

```bash
cat << EOF >> .env
SIGNUPS_ALLOWED=false
EOF
docker-compose down
docker-compose up -d
```

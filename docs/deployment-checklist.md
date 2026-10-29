# Panel + Wings Deployment Checklist

## Infrastructure
- [ ] Choose a supported Ubuntu LTS release for the Panel host.
- [ ] Choose a persistent Linux VPS for each Wings node.
- [ ] Record the Panel and node public IPs privately; do not commit them if they are sensitive.
- [ ] Create DNS A/AAAA records for the Panel and node hostnames.
- [ ] Confirm provider firewall/security-group access.

## Network planning
- [ ] Panel web traffic: TCP 80 and 443.
- [ ] Wings API: use the port configured for the node (commonly TCP 8080, or 8443 when configured for TLS).
- [ ] Game allocations: open only the specific allocation ports you intend to use.
- [ ] Restrict SSH access where practical; never expose database ports publicly without a deliberate secure design.

Ports vary by configuration. Verify the current official documentation and your provider firewall before opening ports.

## Panel
- [ ] Install Panel prerequisites and database/cache dependencies using the official guide.
- [ ] Install the Panel from the official release/source instructions.
- [ ] Configure the database, application key, mail, URL, queue, and cron as documented.
- [ ] Configure a reverse proxy and HTTPS.
- [ ] Create an administrator account.
- [ ] Create a node and define allocations.

## Wings
- [ ] Install Docker and Wings following the official guide for the chosen OS.
- [ ] Generate the node configuration from the Panel's node configuration page.
- [ ] Transfer the configuration securely to the Wings host; it contains credentials.
- [ ] Set correct ownership/permissions and configure Wings as a system service.
- [ ] Start Wings on the VPS and check its service logs.
- [ ] Confirm the node status is online in the Panel.

## Validation
- [ ] Create or import a suitable egg.
- [ ] Create a test server using an allocated port.
- [ ] Verify console, startup, logs, file access, and network connectivity.
- [ ] Test restart behavior and backups.
- [ ] Keep Panel, Wings, Docker, and the OS patched.

## Official references
- https://pterodactyl.io/panel/1.0/getting_started.html
- https://pterodactyl.io/panel/1.0/configuration.html
- https://pterodactyl.io/wings/1.0/installing.html
- https://pterodactyl.io/wings/1.0/configuration.html

## Secrets policy
Never commit .env files, database passwords, application keys, node tokens, SSH keys, or generated Wings configuration. If a secret is accidentally pushed, rotate it; deleting the file alone is not enough.

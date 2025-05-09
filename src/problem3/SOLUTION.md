## Troubleshooting Steps:
- log into the VM via SSH and run `df -h` to confirm the disk usage and identify which filesystem use the most space
- Review the NGINX configuration file (typically /etc/nginx/nginx.conf or files in /etc/nginx/conf.d/) to verify logging settings
- Ensure access_log and error_log are configured appropriately and check if logs are being rotated.
- Confirm that NGINX is only serving as a load balancer and not hosting static files or caching content locally.
- Investigate directories like /tmp, /var/cache/nginx/, or /var/spool/ for temporary or cached files that might be accumulating.
- Use find / -xdev -type f -size +100M to locate unexpectedly large files.
- Verify that log rotation is configured correctly using logrotate (check /etc/logrotate.conf and /etc/logrotate.d/nginx).
- Test log rotation with logrotate -f /etc/logrotate.conf to ensure it’s functioning.

## Expected Causes, Scenarios, Impacts, and Recovery Steps

### NGINX Logging

#### Scenario
NGINX is configured with verbose logging (access_log enabled with detailed formats), and logs are not rotated or compressed, causing /var/log/nginx/access.log or error.log to grow uncontrollably.

#### Recovery Steps
1. Truncate large log files: 
 `/var/log/nginx/access.log` or  `/var/log/nginx/error.log`

2. Configure log rotation in /etc/logrotate.d/nginx
# Scenario 10: Nginx Returns 502 Bad Gateway

## 1. Problem Statement
Nginx returns `502 Bad Gateway` when acting as a reverse proxy to an upstream application.

## 2. Symptoms
- The browser or API client receives HTTP 502.
- Nginx is running, but the proxied application is unavailable.
- Nginx error logs report connection refused, timeout, or an invalid upstream response.

## 3. Possible Root Causes
- The upstream application is stopped or unhealthy.
- Nginx points to the wrong host or port.
- The upstream is not listening on the expected interface.
- DNS resolution or container networking is failing.
- Nginx cannot reach the upstream because of firewall or network rules.
- The upstream closes the connection or returns an invalid response.

## 4. Investigation
Check Nginx service status:
```bash
sudo systemctl status nginx
```

Check configuration syntax:
```bash
sudo nginx -t
```

Review recent error logs:
```bash
sudo tail -n 100 /var/log/nginx/error.log
```

Check listening ports:
```bash
sudo ss -lntp
```

Test the upstream directly from the Nginx host, using the actual upstream address:
```bash
curl -v http://UPSTREAM_HOST:PORT/
```

Check the application service and its logs using the correct service manager or container tooling.

## 5. Resolution
1. Read the Nginx error log to distinguish connection refusal, timeout, DNS failure, and invalid upstream response.
2. Start or repair the upstream service if it is stopped.
3. Correct the upstream host, port, protocol, or DNS configuration.
4. Fix container network configuration or firewall rules if they block communication.
5. Update Nginx configuration only as required, then validate it:
   ```bash
   sudo nginx -t
   ```
6. Reload Nginx after a successful validation:
   ```bash
   sudo systemctl reload nginx
   ```

## 6. Verification
- Request the application through Nginx.
- Confirm the expected HTTP status and response.
- Review Nginx and application logs.
- Check the upstream health and monitor for recurring 502 responses.

## 7. Prevention
- Add upstream health checks where supported.
- Monitor 5xx response rates and application availability.
- Keep upstream addresses and ports documented.
- Use appropriate timeouts based on application behavior.
- Test configuration before reloading Nginx.

## 8. Interview-Ready Explanation
“I would check Nginx status, configuration syntax, and the error log to identify the type of upstream failure. Then I would test the application directly from the Nginx host, verify the upstream address and port, and check service and network health. After fixing the cause, I would validate and reload Nginx and test the public endpoint.”

## 9. Safety Note
Do not increase timeouts or disable security controls without evidence. A 502 is often a symptom of an upstream problem, so investigate the actual error first.

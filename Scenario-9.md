# Scenario 9: Prometheus Target Is Down

## 1. Problem Statement
A Prometheus target shows as `DOWN`, so metrics from a service or exporter are not being collected.

## 2. Symptoms
- The target appears as `DOWN` in Prometheus.
- Metrics from the target are missing or stale.
- Alerts may fire because the target is unreachable.
- Prometheus reports a scrape error.

## 3. Possible Root Causes
- The exporter or application is stopped.
- Incorrect target address or scrape port.
- Network, firewall, or Kubernetes service connectivity issue.
- Incorrect scrape path, scheme, or authentication.
- DNS resolution failure.
- TLS or scrape configuration error.

## 4. Investigation
1. Open Prometheus and inspect **Status → Targets**.
2. Read the target's exact error message and scrape URL.
3. Confirm the exporter or application is running.
4. From the Prometheus host or pod, test connectivity to the target using approved tools:
   ```bash
   curl -v http://TARGET_HOST:PORT/metrics
   ```
   Replace the address and port with the configured values. Use HTTPS if configured.
5. Check Prometheus configuration and logs.
6. In Kubernetes, verify the relevant Service, endpoints, labels, and network policies.

## 5. Resolution
- Start or repair the exporter if it is stopped.
- Correct the target address, port, path, scheme, or service discovery labels.
- Fix the network or firewall rule blocking the scrape.
- Correct TLS or authentication configuration.
- Validate the configuration and reload Prometheus using the environment's supported process.

## 6. Verification
- Confirm the target status becomes `UP`.
- Query a known metric from the target.
- Check that metric timestamps and dashboards update.
- Confirm alerts return to the expected state.

## 7. Prevention
- Monitor `up` and scrape error metrics.
- Alert on targets that remain down.
- Document exporter ports and service discovery.
- Test monitoring changes before rollout.
- Monitor Prometheus itself and retain configuration in version control.

## 8. Interview-Ready Explanation
“I would inspect the target's scrape error in Prometheus, then test the endpoint from the Prometheus environment. I would check exporter health, address and port, network access, service discovery, and TLS or authentication settings. After correcting the cause, I would verify the target is up and metrics are being collected.”

## 9. Safety Note
Do not expose metrics endpoints publicly unless required and protected. Use the configured protocol and authentication rather than weakening security to make a scrape succeed.

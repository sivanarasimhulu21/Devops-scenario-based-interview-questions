# Scenario 2: Linux Server Has High CPU Usage

## 1. Problem Statement
A Linux server experiences sustained high CPU usage, causing slow responses or timeouts for applications.

## 2. Symptoms
- Commands or applications respond slowly.
- Monitoring reports high CPU utilization.
- Requests time out or queues grow.
- Load average remains elevated.

## 3. Possible Root Causes
- A process consuming excessive CPU.
- Too many concurrent requests or jobs.
- An inefficient query, loop, or application task.
- A sudden traffic increase.
- CPU throttling or insufficient allocated CPU resources.

## 4. Investigation
Check load average and uptime:
```bash
uptime
```

View processes sorted by CPU usage:
```bash
top
```

If available, use:
```bash
htop
```

Show processes with CPU and memory usage:
```bash
ps -eo pid,ppid,comm,%cpu,%mem --sort=-%cpu | head
```

Check CPU count:
```bash
nproc
```

Review relevant service logs:
```bash
sudo journalctl -u SERVICE_NAME --since "30 minutes ago"
```
Replace `SERVICE_NAME` with the actual systemd service.

## 5. Resolution
1. Identify the process and determine whether the usage is expected.
2. Correlate CPU usage with application logs, traffic, deployments, and scheduled jobs.
3. If a known job is responsible, pause or reschedule it according to operational procedures.
4. Fix the application, query, or workload causing unnecessary CPU consumption.
5. Scale CPU resources only when evidence shows capacity is insufficient.
6. Avoid killing a production process before understanding its role and impact.

## 6. Verification
- Recheck `top`, `uptime`, and application latency.
- Confirm service health and error rates.
- Verify CPU utilization remains within the expected range after the change.

## 7. Prevention
- Set CPU and latency alerts.
- Establish dashboards and baselines.
- Load-test important services.
- Review scheduled jobs and application performance.
- Use autoscaling where appropriate and properly configured.

## 8. Interview-Ready Explanation
“I would confirm the load and identify the highest-CPU processes using `top` and `ps`. Then I would correlate the process with application logs and recent changes, address the root cause, and verify CPU usage and application latency after the fix. I would also add monitoring and capacity safeguards.”

## 9. Safety Note
High load average does not always mean CPU saturation; tasks waiting for disk I/O can also increase load. Check CPU, memory, and I/O evidence before choosing a fix.

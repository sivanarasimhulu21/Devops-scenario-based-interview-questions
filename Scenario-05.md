# Scenario 5: Docker Container Keeps Restarting

## 1. Problem Statement
A Docker container repeatedly exits and restarts, preventing the application from staying available.

## 2. Symptoms
- `docker ps` shows a restarting container.
- The application endpoint is unavailable.
- Container restart count increases.
- The container logs show startup errors or the process exits.

## 3. Possible Root Causes
- Application startup failure or incorrect command.
- Missing environment variables or configuration.
- Dependency, database, or network connection failure.
- Incorrect file permissions or missing files.
- Memory limit or out-of-memory termination.
- Incorrect health check or restart policy.

## 4. Investigation
List running and stopped containers:
```bash
docker ps -a
```

Inspect recent logs:
```bash
docker logs --tail 200 CONTAINER_NAME
```

Inspect state, exit code, and restart count:
```bash
docker inspect CONTAINER_NAME --format \
'Status={{.State.Status}} ExitCode={{.State.ExitCode}} OOMKilled={{.State.OOMKilled}} RestartCount={{.RestartCount}}'
```

Review configured environment, mounts, ports, and health checks carefully:
```bash
docker inspect CONTAINER_NAME
```

Check resource usage for running containers:
```bash
docker stats --no-stream
```

## 5. Resolution
1. Read the logs and inspect the exit code before changing the container.
2. Correct the application command, configuration, permissions, or dependency issue found.
3. Verify required environment variables and mounted files without exposing secrets.
4. Check memory limits and resource availability if there is evidence of an OOM event.
5. Rebuild the image if the image contents or build process are the cause.
6. Restart or recreate the container using the normal deployment process.

## 6. Verification
- Confirm the container remains running.
- Review logs for successful startup.
- Check the health status and application endpoint.
- Confirm restart count is no longer increasing.

## 7. Prevention
- Use reliable health checks.
- Log startup errors clearly.
- Pin and test image versions.
- Manage secrets outside the image.
- Set suitable resource limits and monitor container restarts.

## 8. Interview-Ready Explanation
“I would inspect container status, logs, exit code, OOMKilled status, and restart count. These clues help distinguish an application startup error from a resource or configuration issue. After fixing the root cause, I would verify the container stays healthy and the application responds.”

## 9. Safety Note
Do not delete volumes or run broad Docker prune commands during troubleshooting without checking whether they contain persistent data or resources used by other workloads.

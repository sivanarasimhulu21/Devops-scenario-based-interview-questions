# Scenario 7: Kubernetes Pod Enters CrashLoopBackOff

## 1. Problem Statement
A Kubernetes pod repeatedly starts and exits, and its status becomes `CrashLoopBackOff`.

## 2. Symptoms
- `kubectl get pods` shows `CrashLoopBackOff`.
- The pod restarts repeatedly.
- The application is unavailable or a deployment has fewer ready replicas than expected.

## 3. Possible Root Causes
- Application process exits due to an error.
- Missing configuration, Secret, or environment variable.
- Failed dependency connection.
- Incorrect command or container image.
- Liveness probe configuration causes repeated restarts.
- Resource limits lead to an OOM kill.

## 4. Investigation
List pods in the correct namespace:
```bash
kubectl get pods -n NAMESPACE
```

Describe the affected pod:
```bash
kubectl describe pod POD_NAME -n NAMESPACE
```

Read current container logs:
```bash
kubectl logs POD_NAME -n NAMESPACE
```

Read logs from the previous container instance:
```bash
kubectl logs POD_NAME -n NAMESPACE --previous
```

Review recent events:
```bash
kubectl get events -n NAMESPACE --sort-by=.metadata.creationTimestamp
```

Inspect deployment configuration and resource settings:
```bash
kubectl describe deployment DEPLOYMENT_NAME -n NAMESPACE
```

## 5. Resolution
1. Use pod events and current/previous logs to identify the failure.
2. Correct the image, command, configuration, Secret reference, or dependency issue as appropriate.
3. If the application is healthy but the probe is incorrect, adjust the probe to reflect actual startup and health behavior.
4. If the container is being OOM-killed, assess memory usage and limits before changing resources.
5. Apply changes through the normal manifest or deployment workflow.

## 6. Verification
```bash
kubectl get pods -n NAMESPACE
kubectl rollout status deployment/DEPLOYMENT_NAME -n NAMESPACE
```
Confirm the pod becomes ready, restarts stop increasing, and the service responds.

## 7. Prevention
- Configure meaningful readiness, liveness, and startup probes.
- Set resource requests and limits based on measured needs.
- Manage configuration and Secrets carefully.
- Monitor pod restarts and deployment health.
- Test images and configuration before production rollout.

## 8. Interview-Ready Explanation
“I would inspect the pod description, events, and current and previous logs. I would use the evidence to distinguish an application crash, configuration issue, dependency failure, probe problem, or OOM kill. After correcting the cause through the deployment configuration, I would verify rollout status and application health.”

## 9. Safety Note
Use the correct cluster and namespace. Avoid deleting production pods or changing resource limits before understanding the cause and impact.

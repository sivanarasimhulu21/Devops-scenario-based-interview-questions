
# SCN-001: Linux Disk Usage Reaches 100%

## 1. Problem Statement

A Linux production server reports 100% disk usage. Applications fail to write files, and services may stop working.

## 2. Environment

- OS: Ubuntu Linux
- Environment: Linux server or cloud VM
- Impact: Applications may fail to write logs or temporary files

## 3. Symptoms

- Disk usage reaches 100%.
- Applications report "No space left on device".
- Log files may stop updating.
- Deployments may fail.

## 4. Investigation

Check filesystem usage:

```bash
df -h
```

Find large directories:

```bash
sudo du -xhd1 / 2>/dev/null | sort -h
```

Check inode usage:

```bash
df -i
```

Find large files:

```bash
sudo find /var/log -type f -size +100M -ls
```

## 5. Possible Root Causes

- Large application or system logs
- Old deployment artifacts
- Unused container images and build cache
- Deleted files still held open by processes
- Inode exhaustion

## 6. Solution

Identify the actual cause before removing files.

- Rotate or safely truncate confirmed oversized logs.
- Remove verified obsolete artifacts.
- Clean unused Docker resources only after reviewing their impact.
- Restart or reload services only when required.

Never delete unknown production files just to free disk space.

## 7. Verification

```bash
df -h
df -i
```

Confirm that the application can write files and that affected services are healthy.

## 8. Prevention

- Configure log rotation.
- Monitor disk and inode usage.
- Set alerts before critical thresholds.
- Review container logs and build-cache retention.
- Establish regular disk-usage reviews.

## 9. Interview-Ready Explanation

First, I check filesystem and inode usage using `df -h` and `df -i`. Then I identify the directories or files consuming space. After confirming the root cause, I clean up only safe, unnecessary data or correct the relevant retention settings. Finally, I verify application health and configure monitoring to prevent recurrence.


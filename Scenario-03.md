# Scenario 3: Linux Server Fails to Boot

## 1. Problem Statement
A Linux server does not complete startup or becomes unavailable after a reboot.

## 2. Symptoms
- The server does not respond over SSH.
- The console shows boot errors, emergency mode, or a kernel panic.
- A filesystem mount fails.
- The system repeatedly reboots or stalls during startup.

## 3. Possible Root Causes
- Incorrect `/etc/fstab` entry or unavailable storage.
- Filesystem corruption.
- A failed kernel or bootloader update.
- Insufficient disk space in a required filesystem.
- Hardware, virtual-machine, or cloud infrastructure issues.

## 4. Investigation
Start with the server's physical, hypervisor, or cloud serial/system console. Record the exact error before changing anything.

If the system reaches a shell, inspect failed units:
```bash
systemctl --failed
```

Review current-boot logs:
```bash
journalctl -xb
```

Check disk and mount configuration where possible:
```bash
df -h
cat /etc/fstab
```

For a cloud VM, also check instance status checks, attached volumes, and provider console output.

## 5. Resolution
1. Preserve console output and identify the first relevant error.
2. If a mount fails, verify the device UUID and mount configuration before editing `/etc/fstab`.
3. If a recent kernel or package update is implicated, use the platform's supported recovery procedure.
4. If filesystem repair is required, follow the filesystem-specific procedure and ensure the filesystem is unmounted when required.
5. Take or verify a recovery snapshot/backup when possible before making disk-level changes.
6. Reboot only after correcting the confirmed issue.

## 6. Verification
- Confirm the server reaches the normal login target.
- Run `systemctl --failed` and review boot logs.
- Verify expected filesystems and services are available.
- Confirm remote access and application health.

## 7. Prevention
- Test changes before production rollout.
- Maintain tested backups and recovery procedures.
- Validate `/etc/fstab` changes and use UUIDs where appropriate.
- Monitor disk space and boot-critical services.
- Document kernel and bootloader recovery steps.

## 8. Interview-Ready Explanation
“I would use the server console to capture the boot error, then inspect systemd and boot logs if a shell is available. I would isolate whether the issue is storage, filesystem, kernel, bootloader, or infrastructure related, apply the appropriate recovery procedure, and verify that the system and its services start normally.”

## 9. Safety Note
Do not run filesystem repair commands against a mounted filesystem unless the tool and filesystem explicitly support that operation. Recovery steps differ by distribution and storage setup.

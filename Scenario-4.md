# Scenario 4: AWS EC2 Instance Is Unreachable

## 1. Problem Statement
An EC2 instance is running, but users cannot connect to it using SSH or reach the application hosted on it.

## 2. Symptoms
- SSH connections time out or are refused.
- A website or API is unavailable.
- EC2 status checks may show a failure.
- The instance appears running in the AWS console.

## 3. Possible Root Causes
- Incorrect security group inbound or outbound rules.
- Network ACL or route-table configuration problems.
- Missing internet gateway or incorrect subnet routing.
- Incorrect public IP address or no public IP.
- SSH daemon, host firewall, or application failure.
- Incorrect username, key pair, or file permissions.
- Instance or underlying infrastructure status-check failure.

## 4. Investigation
1. Check both EC2 instance status checks in the AWS console.
2. Confirm the instance ID, state, subnet, public/private IP, and attached security groups.
3. Verify that the route table matches the intended connectivity design.
4. Review network ACL rules and any host firewall.
5. Confirm the client is using the correct SSH username and key.
6. If console access is available, inspect the operating system and service logs.

From a permitted client, test SSH connectivity:
```bash
ssh -i /path/to/key.pem USERNAME@PUBLIC_IP
```

For a Linux instance, if you have console or alternative access:
```bash
sudo systemctl status ssh
sudo journalctl -u ssh --since "30 minutes ago"
```
On some distributions the service is named `sshd` instead of `ssh`.

## 5. Resolution
- Allow SSH only from the required trusted source IP or approved network.
- Correct route tables, network ACLs, or gateway configuration as appropriate.
- Restore the correct IP or DNS target if it changed.
- Fix the SSH service, host firewall, or application based on evidence.
- Use Systems Manager Session Manager or another approved recovery method when configured.

## 6. Verification
- Confirm the relevant EC2 status checks pass.
- Test SSH from an authorized source.
- Test the application on its intended port.
- Review application logs and health checks.

## 7. Prevention
- Use least-privilege security group rules.
- Prefer Session Manager where appropriate.
- Monitor EC2 status checks and application endpoints.
- Document subnet and route-table design.
- Avoid exposing SSH to the entire internet unless explicitly justified and controlled.

## 8. Interview-Ready Explanation
“I would separate the problem into AWS infrastructure, network path, operating system access, and application layers. I would check EC2 status checks, IP addressing, routes, security groups, network ACLs, and SSH/application services, then fix the confirmed cause and test connectivity again.”

## 9. Safety Note
Do not share private keys or open all ports to `0.0.0.0/0` as a troubleshooting shortcut.

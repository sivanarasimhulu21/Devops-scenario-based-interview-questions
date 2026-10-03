# Scenario 8: Terraform Apply Fails

## 1. Problem Statement
A Terraform configuration fails during `terraform plan` or `terraform apply`, preventing infrastructure changes from completing.

## 2. Symptoms
- Terraform reports an error.
- A provider cannot authenticate or initialize.
- A resource cannot be created or updated.
- The configuration works in one environment but not another.

## 3. Possible Root Causes
- Invalid HCL syntax or incorrect variable values.
- Provider version or initialization problem.
- Missing permissions or expired credentials.
- Resource limits, naming conflicts, or existing resources.
- Incorrect state, concurrent operations, or resource drift.
- Network connectivity or API availability problems.

## 4. Investigation
Check the Terraform version:
```bash
terraform version
```

Initialize providers and modules:
```bash
terraform init
```

Validate configuration:
```bash
terraform validate
```

Review the proposed changes:
```bash
terraform plan
```

Inspect state only when needed and treat its contents as sensitive:
```bash
terraform state list
```

Read the exact error message and identify whether it comes from configuration validation, provider authentication, the cloud API, or state management.

## 5. Resolution
1. Preserve the full error message and identify the failing resource or operation.
2. Correct syntax, variables, provider constraints, or missing permissions as indicated.
3. Check whether a resource already exists and whether it is managed by the current state.
4. For state problems, back up state and follow a reviewed recovery procedure.
5. Re-run `terraform plan` and inspect every proposed change before applying.
6. Apply only after confirming the plan is appropriate for the target environment.

## 6. Verification
- Confirm the apply completes successfully.
- Review outputs and the resulting infrastructure.
- Run a fresh `terraform plan` to check for unexpected changes.
- Verify the deployed service or resource is functioning.

## 7. Prevention
- Review plans before applying.
- Use remote state with locking where supported.
- Pin and manage provider versions.
- Use least-privilege cloud credentials.
- Keep state files and secrets out of public repositories.
- Use code review and separate environments.

## 8. Interview-Ready Explanation
“I would start with the exact Terraform error, then validate the configuration and inspect the plan. I would determine whether the cause is HCL, provider initialization, permissions, an existing resource, or state. After correcting it, I would review the new plan before applying and verify the resulting infrastructure.”

## 9. Safety Note
Never delete or manually edit Terraform state as a first troubleshooting step. State changes can disconnect Terraform from real infrastructure and require a controlled recovery process.

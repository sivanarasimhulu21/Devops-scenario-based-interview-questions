# Scenario 6: Jenkins Pipeline Fails

## 1. Problem Statement
A Jenkins pipeline fails during checkout, build, testing, image creation, publishing, or deployment.

## 2. Symptoms
- A pipeline stage turns red.
- The build log contains an error or non-zero exit code.
- A webhook-triggered build does not start.
- The build works locally but fails on the Jenkins agent.

## 3. Possible Root Causes
- Repository URL, branch, credentials, or webhook configuration issue.
- Missing or incompatible JDK, Maven, Docker, or other tool.
- Failed tests or dependency download problems.
- Insufficient disk space or permissions on the agent.
- Incorrect pipeline syntax or environment variables.
- Registry authentication or deployment configuration failure.

## 4. Investigation
1. Identify the first failing stage and the earliest meaningful error in the console log.
2. Confirm the repository, branch, and commit being built.
3. Check agent availability and configured tool versions.
4. Inspect disk space and permissions on the agent:
   ```bash
   df -h
   ```
5. Run the relevant build command in the same environment where practical, such as:
   ```bash
   java -version
   mvn -version
   ```
6. Check credential IDs and permissions without printing secrets.

## 5. Resolution
- Correct the specific repository, branch, or credential configuration.
- Install or configure the required tool version on the agent.
- Fix compilation or test failures rather than bypassing them without justification.
- Resolve dependency or network access issues.
- Correct file ownership, workspace permissions, or disk capacity as evidenced.
- Fix pipeline syntax or environment variable handling.
- Retry the pipeline after addressing the root cause.

## 6. Verification
- Run the failed stage again.
- Confirm tests and quality checks complete as intended.
- Verify the image or artifact was published to the expected location.
- Confirm deployment health if deployment is part of the pipeline.

## 7. Prevention
- Keep pipeline stages small and clearly named.
- Pin tool versions and use reproducible build environments.
- Store credentials in Jenkins Credentials, not source code.
- Retain useful logs and notify the responsible team.
- Add tests and safe rollback procedures.

## 8. Interview-Ready Explanation
“I would identify the first failing pipeline stage and inspect its console output. Then I would verify the source revision, agent environment, tools, credentials, dependencies, and permissions relevant to that stage. After correcting the root cause, I would rerun the pipeline and verify the produced artifact or deployment.”

## 9. Safety Note
Never paste tokens, passwords, private keys, or secret environment values into logs or public repositories.

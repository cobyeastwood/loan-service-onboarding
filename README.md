Loan Origination Service - Postman Onboarding
This repo hooks up the Loan Origination API spec to the Postman Enterprise Catalog using automated GitHub Actions.

How I built this & key decisions
Dynamic naming: Used ${{ github.event.repository.name }} to automatically use the Postman workspace name to the Git repository name, keeping the pipeline logic clean.

Standardized paths: Maintained the strict specs/openapi.yaml file location pattern to keep the automated ingestion uniform with the rest of the services.

Universal vs. Per Service
Universal: The underlying pipeline framework, checkout steps, permission blocks, and local tracking files are identical across the org.

Per Service: The metadata targets the Lending domain (domain: "lending", domain-code: "LOAN").

What the Ops/Platform team needs to configure
The platform team needs to handle a few specific environment and infrastructure steps for this service:

Compute Infrastructure Auth: Configure security groups inside the Postman environments.

Secrets provisioning: Set up the repo's GitHub Actions Secrets with the required Postman API credentials.

How to run, validate, and trade-offs
To run: Push an update to specs/openapi.yaml on the main branch, or manually trigger the workflow from the Actions tab.

Validation: Verify the postman/ directory is successfully created and committed back to the repo root. Check the Postman account to confirm the workspace is visible.

Trade-offs: Same as the payments service, the pipeline uses a YAML schema rather than JSON.

AI Usage & Debugging
What AI did: Used AI to scaffold the base workflow configuration and help think through the architectural mapping for the GitLab CI blocker.

What I wrote/validated manually: I handled the actual end to end execution testing against my Postman account. I manually configured the repository tokens, tested the workflow by running it through multiple manual reruns to ensure it updated in postman properly, and verified that the YAML outputs correctly mapped inside Spec Hub.

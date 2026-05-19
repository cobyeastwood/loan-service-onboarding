# Loan Origination Service - Postman Onboarding

This repository automates onboarding the Loan Origination API specification into Postman using GitHub Actions.

---

## Key Design Decisions

- **Dynamic Naming:** Uses `${{ github.event.repository.name }}` to automatically derive the Postman workspace name from the Git repository, keeping the workflow reusable.
- **Standardized Paths:** Locks the specification file to `specs/openapi.yaml` for ingestion.
- **Universal vs. Per-Service:** The framework and triggers are identical across services, while the repository secrets and Postman catalog metadata point specifically to the Lending domain.

## AWS Configuration Prerequisites

The following parameters must be configured on the AWS side to support the loan service onboarding workflow:

- **Base URLs:** Map the active regional endpoints for the Application Load Balancer (ALB) stages specified in the [loan-origination-api-openapi.yaml](https://github.com/postman-cs/cse-exercise/blob/main/specs/loan-origination-api-openapi.yaml) spec (e.g., Staging: `https://lending-api-staging.example.com/v1`, Dev: `https://lending-api-dev.example.com/v1`).
- **Test Tokens & Certificates:** Provide valid mock credentials matching the service's security architecture to populate Postman variables:
  - **mTLS Layer:** Provide valid client certificates and keys to configure Postman's global Settings/Certificates for handshake validation.
  - **JWT:** Internal service-to-service tokens containing the `refunds` scope.
  - **Network & VPC Access:** If the application is hosted through a cloud provider, ensure your security groups are configured to allow inbound traffic from GitHub runner and Postman agent IP addresses.

## Execution & Validation

- **To Run:** Push an update to `specs/openapi.yaml` on the `main` branch, or manually trigger the workflow from the Actions tab.
- **Validation:** Verify that the `postman/` directory is generated and committed back to the repo root, and confirm the corresponding workspace is visible in the Postman UI.

## AI Transparency & Debugging

- **AI Generation:** Used an AI assistant to scaffold the base workflow configuration and structure the architectural mapping for the GitLab CI alternative.
- **Manual Validation:** Handled the end-to-end execution testing against a live Postman account. Manually configured the repository tokens, executed consecutive manual reruns to verify consistent workspace updates, and validated that the collections correctly mapped inside Spec Hub.

# EC2 Domain Join Automation

This repository contains an AWS Systems Manager (SSM) document that automates the process of joining EC2 instances to a custom Active Directory domain.  It leverages PowerShell for the domain join operation and securely retrieves domain credentials from AWS Secrets Manager.

## Key Features

* **Secure Credential Management:** Domain join credentials are stored securely in AWS Secrets Manager and retrieved at runtime. This prevents sensitive information from being embedded in the SSM document.
* **PowerShell-based Domain Join:** Uses PowerShell's `Add-Computer` cmdlet for a robust and flexible domain join process.
* **Connectivity Test:** Includes a test to verify network connectivity to `canaldigital.com` on port 389 (LDAP). This helps diagnose potential network issues.
* **Domain Join Validation:**  Validates the domain join by checking the instance's domain membership.  This ensures the process was successful.
* **Automated and Scalable:** The SSM document can be run against multiple EC2 instances, making domain join automation scalable and efficient.

## Prerequisites

Before using this SSM document, ensure the following prerequisites are met:

1. **Active Directory Domain:** You must have a functioning Active Directory domain.

2. **AWS Secrets Manager Secret:** Create a secret in AWS Secrets Manager containing the domain join credentials. The secret should be a JSON object with the following keys:

   ```json
   {
     "username": "domain_join_user",
     "password": "domain_join_password"
   }

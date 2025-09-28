## User Management & Security Implementation

### 2.1 Create IAM Users and Groups

**Create Developer User:**
```bash
aws iam create-user --user-name techstart-developer
aws iam create-group --group-name TechStartDevelopers
aws iam add-user-to-group --user-name techstart-developer --group-name TechStartDevelopers
```

**Create Admin User:**
```bash
aws iam create-user --user-name techstart-admin
aws iam create-group --group-name TechStartAdmins
aws iam add-user-to-group --user-name techstart-admin --group-name TechStartAdmins
```

<img width="1919" height="620" alt="Screenshot 2025-09-28 194924" src="https://github.com/user-attachments/assets/2e8715de-2f93-446a-9bd9-add4646de44c" />


### 2.2 Create KMS Key for Encryption

**Console Method:**
1. Navigate to KMS → Create Key
2. **Key Type**: Symmetric
3. **Key Usage**: Encrypt and decrypt
4. **Alias**: `techstart-main-key`
5. **Key Policy**: Default settings

<img width="1918" height="641" alt="Screenshot 2025-09-28 195010" src="https://github.com/user-attachments/assets/0ec56d87-aa8d-4320-85fa-51922ce54a13" />


**CLI Method:**
```bash
aws kms create-key --description "TechStart main encryption key"
aws kms create-alias --alias-name alias/techstart-main-key --target-key-id [KEY-ID]
```

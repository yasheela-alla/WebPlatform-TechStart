## Data Storage Solutions Implementation:

### 3.1 Create S3 Buckets

**User Assets Bucket:**
```bash
# Replace [timestamp] with current timestamp
aws s3 mb s3://techstart-user-assets-$(date +%s) --region us-east-1
```

**Application Backups Bucket:**
```bash
aws s3 mb s3://techstart-app-backups-$(date +%s) --region us-east-1
```

<img width="1918" height="750" alt="Screenshot 2025-09-28 195043" src="https://github.com/user-attachments/assets/c2c937e2-bb16-4b4c-9990-4e02e266b22e" />


### 3.2 Create DynamoDB Tables

**Customers Table:**
```bash
aws dynamodb create-table \
    --table-name Customers \
    --attribute-definitions AttributeName=CustomerID,AttributeType=S \
    --key-schema AttributeName=CustomerID,KeyType=HASH \
    --billing-mode PAY_PER_REQUEST \
    --region us-east-1
```

**Products Table:**
```bash
aws dynamodb create-table \
    --table-name Products \
    --attribute-definitions AttributeName=ProductID,AttributeType=S \
    --key-schema AttributeName=ProductID,KeyType=HASH \
    --billing-mode PAY_PER_REQUEST \
    --region us-east-1
```

<img width="973" height="475" alt="Screenshot 2025-09-28 195124" src="https://github.com/user-attachments/assets/46344c85-508a-4648-be7d-eaee694d7a32" />


### 3.3 Create RDS MySQL Database

**Console Method:**
1. Navigate to RDS → Create Database
2. **Engine**: MySQL
3. **Template**: Sandbox (Single-AZ)
4. **DB Identifier**: `techstart-main-db`
5. **Master Username**: `admin`
6. **Master Password**: `TechStart2024!`
7. **Instance Class**: `db.t3.micro`
8. **Storage**: General Purpose SSD
9. **Public Access**: No

<img width="1898" height="909" alt="Screenshot 2025-09-28 195216" src="https://github.com/user-attachments/assets/3127b0c6-373d-4d94-ac71-d59c426c0fe0" />


**CLI Method:**
```bash
aws rds create-db-instance \
    --db-instance-identifier techstart-main-db \
    --db-instance-class db.t3.micro \
    --engine mysql \
    --master-username admin \
    --master-user-password TechStart2024! \
    --allocated-storage 20 \
    --vpc-security-group-ids sg-default
```

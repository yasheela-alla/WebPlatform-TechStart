# TechStart Inc. - Complete AWS Cloud Platform

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![MySQL](https://img.shields.io/badge/mysql-%2300f.svg?style=for-the-badge&logo=mysql&logoColor=white)

> **KodeKloud Hands-on Project**: Build a Complete Web Platform for TechStart Inc.
> 
> **Duration**: 45-60 minutes | **Level**: Intermediate

## 📖 Project Story

TechStart Inc. is a new startup that needs to launch their web platform quickly and securely. As their cloud architect, you need to set up the entire infrastructure including web hosting, user management, data storage, monitoring, and security. The CEO wants everything ready for their product launch in 2 hours!

<img width="1919" height="1034" alt="Screenshot 2025-09-28 182213" src="https://github.com/user-attachments/assets/5c023155-ee9c-4db1-af29-0e50380e6fa0" />



## ✅ Requirements

- [x] Secure web server to host the application with public IP access
- [x] User authentication and access management system with proper IAM roles
- [x] Database to store customer and product information (NoSQL + SQL)
- [x] File storage for user uploads and assets with backup strategy
- [x] Monitoring and alerting system with real-time dashboards
- [x] Automated notification system for customer engagement via Lambda

## 🚀 Project Phases

### Phase 1: Infrastructure ✅
- [x] EC2 instance running with public IP assigned
- [x] Instance properly tagged and accessible

### Phase 2: Security ✅  
- [x] IAM users created (`iamuser-dev-lead`, `iamuser-ops-admin`)
- [x] KMS key active with proper alias
- [x] Security policies implemented

### Phase 3: Data Storage ✅
- [x] S3 buckets accessible (user-assets, app-backups)
- [x] DynamoDB tables active (Customers, Products)  
- [x] RDS MySQL database available and configured

### Phase 4: Automation & Monitoring ✅
- [x] Lambda function tested and operational
- [x] SQS/SNS messaging services configured
- [x] CloudWatch dashboard displaying real-time metrics

<img width="1915" height="1039" alt="Screenshot 2025-09-28 200254" src="https://github.com/user-attachments/assets/f1f54032-c542-4d48-a3e9-4028e8e0d8c6" />

## 💸 Cost Optimization

- **Free Tier Resources**: Use t3.micro instances, 750 hours/month
- **DynamoDB**: Pay-per-request billing for variable workloads
- **S3**: Lifecycle policies for automated archival to cheaper storage classes
- **Monitoring**: AWS Cost Explorer and billing alerts setup
- **Resource Cleanup**: Automated scripts to remove unused resources


## 🛠️ Troubleshooting Guide

### Common Issues

**Permission Denied Errors:**
```bash
# Check current user permissions
aws sts get-caller-identity
aws iam list-attached-user-policies --user-name $(aws sts get-caller-identity --query User.UserName --output text)
```

**Resource Limits:**
```bash
# Check service quotas
aws service-quotas list-service-quotas --service-code ec2
aws service-quotas list-service-quotas --service-code rds
```

**Region Availability:**
```bash
# Verify service availability in region
aws ec2 describe-regions --query 'Regions[?RegionName==`us-east-1`]'
```

---

**❤️you KodeKloud**

*Happy Learning! 🎓*

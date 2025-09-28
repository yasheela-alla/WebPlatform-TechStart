## Infrastructure Setup & Web Server Deployment

### 1.1 Verify AWS Environment
```bash
# Check available regions and AZs
aws ec2 describe-regions --query 'Regions[].RegionName' --output table
aws ec2 describe-availability-zones --region us-east-1 --query 'AvailabilityZones[].ZoneName' --output table
```

### 1.2 Launch EC2 Web Server

**Console Method:**
1. Navigate to EC2 → Launch Instance
2. **Name**: `TechStart-WebServer`
3. **AMI**: Amazon Linux 2023 AMI
4. **Instance Type**: `t3.micro` (Free tier)
5. **Key Pair**: Proceed without key pair
6. **Security Group**: Default (SSH access)
7. **Storage**: 8GB gp3 root volume
8. Launch instance


<img width="1919" height="975" alt="Screenshot 2025-09-28 194832" src="https://github.com/user-attachments/assets/a1a9755d-aedd-4f6f-b28a-422722c92627" />

---

***CLI Method:***
```bash
aws ec2 run-instances \
    --image-id ami-0abcdef1234567890 \
    --instance-type t3.micro \
    --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=TechStart-WebServer}]' \
    --security-group-ids sg-default
```

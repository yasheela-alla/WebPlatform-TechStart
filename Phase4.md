## Automation & Monitoring Systems:

### 4.1 Lambda Function for Customer Welcome Emails

Create `lambda_function.py`:

```python
import json

def lambda_handler(event, context):
    """
    CustomerWelcomeEmail Lambda Function
    Automatically sends welcome emails to new TechStart customers
    """
    
    # Extract customer information from the event
    customer_id = event.get('customer_id', 'Unknown')
    customer_email = event.get('email', 'noemail@example.com')
    customer_name = event.get('name', 'Valued Customer')
    
    # Simulate sending welcome email
    welcome_message = f"""
    Welcome to TechStart Inc., {customer_name}!
    
    Thank you for joining our platform. Your customer ID is: {customer_id}
    
    We're excited to have you on board!
    
    Best regards,
    The TechStart Team
    """
    
    # Log the welcome email (in production, this would integrate with SES)
    print(f"Sending welcome email to {customer_email}")
    print(f"Message: {welcome_message}")
    
    # Return success response
    return {
        'statusCode': 200,
        'body': json.dumps({
            'message': f'Welcome email sent successfully to {customer_email}',
            'customer_id': customer_id,
            'timestamp': context.aws_request_id
        })
    }
```
<img width="1898" height="909" alt="Screenshot 2025-09-28 195216" src="https://github.com/user-attachments/assets/14bd7cbe-e580-418f-aa00-c191fd24a11c" />


**Deploy Lambda Function:**

**Console Method (Recommended):**
1. Navigate to Lambda → Create Function
2. **Function Name**: `CustomerWelcomeEmail`
3. **Runtime**: Python 3.11
4. **Architecture**: x86_64
5. **Execution Role**: Create new role with basic Lambda permissions
6. Replace default code with the function code above
7. Click **Deploy**

**CLI Method:**
```bash
# Package function
zip lambda_function.zip lambda_function.py

# Create function
aws lambda create-function \
    --function-name CustomerWelcomeEmail \
    --runtime python3.11 \
    --role arn:aws:iam::ACCOUNT:role/lambda-execution-role \
    --handler lambda_function.lambda_handler \
    --zip-file fileb://lambda_function.zip
```

**Test Lambda Function:**
```bash
# Test with sample data
aws lambda invoke \
    --function-name CustomerWelcomeEmail \
    --payload '{"customer_id":"CUST001","email":"john@example.com","name":"John Doe"}' \
    --cli-binary-format raw-in-base64-out \
    output.txt
```

<img width="1919" height="1029" alt="Screenshot 2025-09-28 195626" src="https://github.com/user-attachments/assets/3d23d40f-fc88-4e90-8a73-2995de9c775b" />


#### 4.2 Create Messaging Services

**SQS Queue for Order Processing:**
```bash
aws sqs create-queue \
    --queue-name order-processing-queue \
    --region us-east-1
```

**SNS Topic for Team Alerts:**
```bash
aws sns create-topic \
    --name TechStart-Alerts \
    --region us-east-1
```

#### 4.3 CloudWatch Monitoring Dashboard

Create `dashboard.json`:
```json
{
    "widgets": [
        {
            "type": "metric",
            "x": 0,
            "y": 0,
            "width": 12,
            "height": 6,
            "properties": {
                "metrics": [
                    [ "AWS/EC2", "CPUUtilization", "InstanceId", "[INSTANCE-ID]" ],
                    [ ".", "NetworkIn", ".", "." ],
                    [ ".", "NetworkOut", ".", "." ]
                ],
                "view": "timeSeries",
                "stacked": false,
                "region": "us-east-1",
                "title": "TechStart WebServer Performance",
                "period": 300
            }
        },
        {
            "type": "metric",
            "x": 12,
            "y": 0,
            "width": 12,
            "height": 6,
            "properties": {
                "metrics": [
                    [ "AWS/Lambda", "Duration", "FunctionName", "CustomerWelcomeEmail" ],
                    [ ".", "Invocations", ".", "." ],
                    [ ".", "Errors", ".", "." ]
                ],
                "view": "timeSeries",
                "stacked": false,
                "region": "us-east-1",
                "title": "Lambda Performance",
                "period": 300
            }
        }
    ]
}
```

**Deploy Dashboard:**
```bash
aws cloudwatch put-dashboard \
    --dashboard-name TechStart-Infrastructure-Dashboard \
    --dashboard-body file://dashboard.json
```
<img width="1919" height="999" alt="Screenshot 2025-09-28 195723" src="https://github.com/user-attachments/assets/26524015-e8c2-4786-b15b-b4fa8dc19efb" />



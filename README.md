Answer the following:
What is needed to authorize your EC2 to retrieve secrets from the AWS Secret Manager?


```M role with IAM policy is need to grant the required premissions. the policy should include action for the secret's ARN.```

Derive the IAM policy (i.e. JSON)?
Using the secret name prod/cart-service/credentials, derive a sensible ARN as the specific resource for access

```python
```{
```
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "secretsmanager:GetSecretValue",
      "Resource": "arn:aws:secretsmanager:ap-southeast-1:255945442255:secret:prod/cart-service/credentials"
    }
  ]
}
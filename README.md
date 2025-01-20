# Assignment 2.14 and 2.15 and 2.16

Answer the following:
- Does SNS guarantee exactly once delivery to subscribers?

```It is not guarantee, a SQS FIFO queue has to exists and with the correct permissions```

- What is the purpose of the Dead-letter Queue (DLQ)? This a feature available to SQS/SNS/EventBridge.

``` Dead-letter Queue exist to improve the reliability and fault-tolerance of your applications by handling messages that could not be processed successfully```

- How would you enable a notification to your email when messages are added to the DLQ?

```you can use Amazon CloudWatch Alarms in combination with Amazon SNS```


Answer the following:
What is needed to authorize your EC2 to retrieve secrets from the AWS Secret Manager?


```M role with IAM policy is need to grant the required premissions. the policy should include action for the secret's ARN.```

Derive the IAM policy (i.e. JSON)?
Using the secret name prod/cart-service/credentials, derive a sensible ARN as the specific resource for access

```python
```{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "secretsmanager:GetSecretValue",
      "Resource": "arn:aws:secretsmanager:ap-southeast-1:255945442255:secret:prod/cart-service/credentials"
    }
  ]
}

Requirements:

Given the Lambda function and metric filters created in the activity, use terraform to create the alarm. Create a public github repository that has a terraform code, containing the answer to the above. Submission is the url to your public github repository.

```
resource "aws_cloudwatch_metric_alarm" "cloudwatch_alarm" { alarm_name = "wx-info-count-breach" comparison_operator = "GreaterThanThreshold" evaluation_periods = 1 metric_name = "info-count" namespace = "/moviedb-api/wx" period = 60 statistic = "Sum" threshold = 10 alarm_description = " " actions_enabled = "true" alarm_actions = [aws_sns_topic.topic.arn] }
resource "aws_sns_topic" "topic" { name = "wx_CloudWatch_Alarms_Topic" }
resource "aws_sns_topic_subscription" "email-target" { topic_arn = aws_sns_topic.topic.arn protocol = "email" endpoint = "thisisweixiong@gmail.com" }

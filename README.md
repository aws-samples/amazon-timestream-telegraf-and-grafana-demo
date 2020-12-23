## Amazon Timestream with Telegraf and Grafana Demo
The purpose of this repository is to demo how to ingest time series data in this case Amazon EC2 instance metrics such as CPU, Memory, Disk into Amazon Timestream.

AWS CloudFormation template (main.yaml) will also deploy an Amazon EC2 instance with Grafana.

###  Launch the AWS CloudFormation Stack

Click on the **Launch Stack** button below to launch the CloudFormation Stack to set up the Amazon Timestream with Telegraf Sample in the region of your preference, by default this demo will be deployed in us-west-2 (Oregon) region.

[![Launch CFN stack](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/quickcreate?templateUrl=https%3A%2F%2Famazon-timestream-telegraf-sample.s3-us-west-2.amazonaws.com%2Fmain.yaml&stackName=timestream-telegraf&param_AllowedIP=0.0.0.0%2F0&param_LatestAmiId=%2Faws%2Fservice%2Fami-amazon-linux-latest%2Famzn2-ami-hvm-x86_64-gp2&param_PublicSubnet1CIDR=10.10.10.0%2F24&param_PublicSubnet2CIDR=10.10.11.0%2F24&param_ResourceName=telegraf-to-timestream&param_VpcCIDR=10.10.0.0%2F16)

Provide a stack name eg **timestream-telegraf**.

You can launch the same stack using the AWS CLI. Here's an example:

```
aws cloudformation create-stack --stack-name timestream-telegraf \
   --template-body file://main.yaml \
   --capabilities CAPABILITY_NAMED_IAM \
   --region us-west-2
```

### Accessing Grafana

Once stack creation is completed, it will output the Application Load Balancer DNS Name under "Outputs" tab of your stack. Another way of accessing via CLI:

```
aws cloudformation describe-stacks --stack-name timestream-telegraf \
   --query "Stacks[0].Outputs[0].OutputValue" \
   --region us-west-2
```

**Username:** ```admin```
**Password:** ```admin```

###  Clean up
After completing your demo, delete AWS CloudFormation Stack using AWS Console or AWS CLI:
```
aws cloudformation delete-stack --stack-name timestream-telegraf  --region us-west-2
```

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

# Deep Security for AWS Elastic Beanstalk

Scripts to deploy and activate the Deep Security agent via [AWS Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/).

## Support

This is a community project and while you will see contributions from the Deep Security team, there is no official Trend Micro support for this project. The official documentation for the Deep Security APIs is available from the [Trend Micro Online Help Centre](http://docs.trendmicro.com/en-us/enterprise/deep-security.aspx). 

Tutorials, feature-specific help, and other information about Deep Security is available from the [Deep Security Help Center](https://help.deepsecurity.trendmicro.com/Welcome.html). 

For Deep Security specific issues, please use the regular Trend Micro support channels. For issues with the code in this repository, please [open an issue here on GitHub](https://github.com/deep-security/elastic-beanstalk/issues).

## Usage 

To integrate Deep Security Agent into the AWS Elastic Beanstalk configuration:

1. Edit the Deep Security Agent AWS Elastic Beanstalk extension configuration file for your operating system to match your Deep Security deployment
1. Add the configuration file to the ```.ebextensions``` directory of your source bundle.
1. Re-deploy your application and your servers will automatically download the latest Agent and activate into the list of instances on the Computers page in Deep Security. 

### Using The .ebextension With Deep Security as a Service

To configure the .ebextension for use with [Deep Security as a Service](https://app.deepsecurity.trendmicro.com/SignIn.screen), you will need to replace 3 items in the appropriate .ebextension. Each of these items is in the final command in the extension (the activation step for the Deep Security agent).

As seen in the [Amazon Linux extension](deep-security-as-a-service/99deepsecurity-as-a-service-amzn1-x86_64.config.ebextension#L9)

```command: '/opt/ds_agent/dsa_control -a dsm://agents.deepsecurity.trendmicro.com:443/ "tenantID:REPLACE-WITH-YOUR-TENANT-ID" "token:REPLACE-WITH-YOUR-TENANT-PASSWORD" "policyid:REPLACE-WITH-YOUR-POLICY-ID" --max-dsm-retries 0 >/tmp/dsa_control.log 2>&1'```

1. ```"tenantID:REPLACE-WITH-YOUR-TENANT-ID"```
1. ```"token:REPLACE-WITH-YOUR-TENANT-PASSWORD"```
1. ```"policyid:REPLACE-WITH-YOUR-POLICY-ID"```

You can find this information within the Deep Security Manager console under **Support > Deployment Scripts**. This dialog will allow you to create a customized deployment script that contains these values.

### Using The .ebextension With Deep Security

To configure the .ebextension for use with your own Deep Security deployment, you will need to replace 3 items in the appropriate .ebextension. These items is in the final command in the extension (the activation step for the Deep Security agent).

As seen in the [Amazon Linux extension](deep-security/99deepsecurity-amzn1-x86_64.config.ebextension#L9)

```
commands:
  00download:
    command: 'wget https://REPLACE-WITH-YOUR-DSM-IP:4119/software/agent/amzn1/x86_64/ -O /tmp/agent.rpm --quiet --no-check-certificates`'
...
  03activate:
    command: '/opt/ds_agent/dsa_control -a dsm://REPLACE-WITH-YOUR-DSM-IP:4120/ "policyid:REPLACE-WITH-YOUR-POLICY-ID" --max-dsm-retries 0 >/tmp/dsa_control.log 2>&1'
```

1. in ```00download:```, ```https://REPLACE-WITH-YOUR-DSM-IP:4119```
1. in ```03activate:```, ```dsm://REPLACE-WITH-YOUR-DSM-IP:4120/```
1. in ```03activate:```, ```"policyid:REPLACE-WITH-YOUR-POLICY-ID"```

You can find this information within the Deep Security Manager console under **Support > Deployment Scripts**. This dialog will allow you to create a customized deployment script that contains these values.

## Support

This is an Open Source community project. Project contributors may be able to help, 
depending on their time and availability. Please be specific about what you're 
trying to do, your system, and steps to reproduce the problem.

For bug reports or feature requests, please 
[open an issue](../issues). 
You are welcome to [contribute](#contribute).

Official support from Trend Micro is not available. Individual contributors may be 
Trend Micro employees, but are not official support.

## Contribute

We accept contributions from the community. To submit changes:

1. Fork this repository.
1. Create a new feature branch.
1. Make your changes.
1. Submit a pull request with an explanation of your changes or additions.

We will review and work with you to release the code.

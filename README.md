# CDK EC2 Key Pair

[![Source](https://img.shields.io/badge/Source-GitHub-blue?logo=github)][source]
[![Test](https://github.com/udondan/cdk-ec2-key-pair/workflows/Test/badge.svg)](https://github.com/udondan/cdk-ec2-key-pair/actions?query=workflow%3ATest)
[![GitHub](https://img.shields.io/github/license/udondan/cdk-ec2-key-pair)][license]
[![Docs](https://img.shields.io/badge/awscdk.io-cdk--ec2--key--pair-orange)][docs]

[![npm package](https://img.shields.io/npm/v/cdk-ec2-key-pair?color=brightgreen)][npm]
[![PyPI package](https://img.shields.io/pypi/v/cdk-ec2-key-pair?color=brightgreen)][PyPI]
[![NuGet package](https://img.shields.io/nuget/v/CDK.EC2.KeyPair?color=brightgreen)][NuGet]

![Downloads](https://img.shields.io/badge/-DOWNLOADS:-brightgreen?color=gray)
[![npm](https://img.shields.io/npm/dt/cdk-ec2-key-pair?label=npm&color=blueviolet)][npm]
[![PyPI](https://img.shields.io/pypi/dm/cdk-ec2-key-pair?label=pypi&color=blueviolet)][PyPI]
[![NuGet](https://img.shields.io/nuget/dt/CDK.EC2.KeyPair?label=nuget&color=blueviolet)][NuGet]

[AWS CDK] L3 construct for managing [EC2 Key Pairs].

CloudFormation doesn't directly support creation of EC2 Key Pairs. This construct provides an easy interface for creating Key Pairs through a [custom CloudFormation resource]. The private key is stored in [AWS Secrets Manager].

## Usage

```typescript
import cdk = require('@aws-cdk/core');
import ec2 = require('@aws-cdk/aws-ec2');
import { KeyPair } from 'cdk-ec2-key-pair';

// Create the Key Pair
const key = new KeyPair(this, 'A-Key-Pair', {
    name: 'a-key-pair',
    description: 'This is a Key Pair',
});

// Grant read access to the private key to a role or user
key.grantRead(someRole)

// Use Key Pair on an EC2 instance
new ec2.Instance(this, 'An-Instance', {
    keyName: key.name,
    // ...
})
```

The private key will be stored in AWS Secrets Manager. The secret name by default is prefixed with `ec2-private-key/`, so in this example it will be saved as `ec2-private-key/a-key-pair`.

To download the private key via AWS cli you can run:

```bash
aws secretsmanager get-secret-value \
  --secret-id ec2-private-key/a-key-pair \
  --query SecretString \
  --output text
```

## Roadmap

- Name should be optional

   [AWS CDK]: https://aws.amazon.com/cdk/
   [custom CloudFormation resource]: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-custom-resources.html
   [EC2 Key Pairs]: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html
   [AWS Secrets Manager]: https://aws.amazon.com/secrets-manager/
   [npm]: https://www.npmjs.com/package/cdk-ec2-key-pair
   [PyPI]: https://pypi.org/project/cdk-ec2-key-pair/
   [NuGet]: https://www.nuget.org/packages/CDK.EC2.KeyPair/
   [docs]: https://awscdk.io/packages/cdk-ec2-key-pair@1.6.0
   [source]: https://github.com/udondan/cdk-ec2-key-pair
   [license]: https://github.com/udondan/cdk-ec2-key-pair/blob/master/LICENSE

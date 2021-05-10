# aws-switcher
Set the default AWS profile in all your shells instantly

# Usage
`aws-switcher`

# Configuration
AWS switcher looks for a `config.yml` in `~/.aws/`.
 
It expects a list of accounts, each account can have the following options:  
| Name | Type | Required | Description |
-|-|-|-
|`name `|String|Yes|A friendly name presented when picking an account and optionally in your bash prompt.|
|`profile`|String|Yes|The profile name to write it out as in ~/.aws/credentials. `source_profile` uses this as the value.|
|`region`|String|Yes|The default region you would like to use.|
|`aws_access_key_id`|String||The AWS access key id you use to access the API. Required if you don't specify `source_profile`.|
|`aws_secret_access_key`|String||The AWS secret access key you use to access the API. Required if you don't specify `source_profile`.|
|`mfa_arn`| String||The ARN of the MFA device you use when authenticating.|
|`source_profile`|String||The profile you want to authenticate with before assuming to the role specified by `role_arn`.|
|`role_arn`|String||The ARN of the role you want to assume.|

# Example
```
- name: Acme Widgets
  profile: acme-main
  region: us-east-1
  aws_access_key_id: aaaa
  aws_secret_access_key: bbbb
- name: Acme Widgets Dev
  profile: acme-dev
  region: us-east-1
  source_profile: acme-main
- name: Acme Widgets Prod
  profile: acme-prod
  region: us-east-1
  source_profile: acme-main
  mfa_arn: arn:aws:iam::123123123123:mfa/acme
- name: Personal account east
  profile: personal
  region: us-east-1
  aws_access_key_id: cccc
  aws_secret_access_key: dddd
- name: Personal account west
  profile: personal
  region: us-west-1
  aws_access_key_id: cccc
  aws_secret_access_key: dddd
```

# Bash prompt
The script writes out the name and region to `~/.aws/status`. The format is `name region`. Using fourth entry in the example config it would look like `Personal account us-east-1`. You could add the following to your `PS1` variable `(AWS: $(cat ~/.aws/status))` to be able to see which profile is active, and for what region.

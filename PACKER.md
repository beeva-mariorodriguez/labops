# PACKER

## packer vs aws
packer does not directly support MFA, so we need to generate a temporal token using aws cli:
```sh
aws sts assume-role \
    --role-arn "ROLE ARN" \
    --role-session-name "Packer"  \
    --profile beeva \
    --token-code "code from your MFA app" \
    --serial-number "YOUR MFA ARN"
export AWS_ACCESS_KEY_ID="AccessKeyId from aws sts ..."
export AWS_SECRET_ACCESS_KEY="SecretAccessKey from aws sts ..."
export AWS_SESSION_TOKEN="SessionToken from aws sts ..."
```
## packer template

substitute the variables with the name and version of the experiment:
```json
{
    "variables": {
        "version": "0.1",
        "experiment": "test"
    },
    "builders":[{
        "type": "amazon-ebs",
        "region": "eu-west-2",
        "source_ami": "ami-f1d7c395",
        "instance_type": "t2.micro",
        "ami_name": "ubuntu-beevalabs-{{ user `experiment` }}-{{ user `version` }}",
        "ssh_username": "ubuntu",
        "tags":{
            "OS_Version": "Ubuntu",
            "Release": "16.04"
        }
    }],
    "provisioners":[{
        "type": "shell",
        "command": "sudo apt install -y ansible"
    },{
        "type": "ansible",
        "playbook_file": "./ansible/playbook.yml"
    }]
}
```

## run packer
```sh
packer build packer-template.json
```


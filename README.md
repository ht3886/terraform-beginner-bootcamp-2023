# Terraform Beginner Bootcamp 2023

## Semantic Versioning :mage:

This project is going to utilize semantic versioning for its tagging.
[semver.org](https://semver.org/)

The general format: **MAJOR.MINOR.PATCH**, eg. ``1.0.1``

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes
Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

## Install the Terraform CLI

### Considerations with the Terraform CLI changes

The Terraform CLI installation instructions have changed due to gpg keyring changes. So I needed to refer to the latest install CLI instructions via Terraform Documentation and change the scripting for install.

[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

### Considerations for Linux Distribution

This project is built against Ubuntu.
Please consider checking your Linux Distribution and change accordingly to distribution needs.

### Refactoring into Bash scripts

While fixing the Terraform CLI gpg documentation issues, I noticed that bash scripts were a considerable amount of extra code. So I decided to create a bash script to install the Terraform CLI.

This bash script is located here: [./bin/install_terraform_cli](./bin/install_terraform_cli)

 - This will keep the GitPod task file tidy. ([gitpod.yml](.gitpod.yml))
 - This allows us an easier way to debug and execute manually Terraform CLI install.
 - This will allow better portability for other projects that need to install Terraform CLI.


#### Shebang considerations

It tells the bash script what program that will interpret the script.
[Shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))

#### Execution Considerations

When executing the bash script we can use the `./` shorthand notation to execute the bash script.

eg: `./bin/install_terraform_cli`

If we are using a script in .gitpod.yml we need to point the script to a program to interpret it.

eg: `source ./bin/install_terraform_cli`

#### Linux Permissions considerations

In order to make our bash scripts executable, we need to change Linux permissions for the fix to be executable at the user mode.

```sh
chmod u+x ./bin/install_terraform_cli
```

alternatively:

```sh
chmod 744 ./bin/install_terraform_cli
```

[chmod](https://en.wikipedia.org/wiki/Chmod)

### GitPod Lifecycle (Before, Init, Command)

We need to be careful when using the Init because it will not return if we restart an existing workspace.
https://www.gitpod.io/docs/configure/workspaces/tasks

### Working with Env vars

#### env command

We can list out all the Environment Variables (Env Vars) using the `env` command

We can filter specific env vars using grep, eg: `env | grep AWS`

#### Setting and Unsetting Env Vars

In the terminal, we can set them using export, eg: `export HELLO = 'world'`

In the terminal, we can unset them using unset, eg: `unset HELLO`

We can set the env var temporarily when just running a command

```sh
HELLO='world' ./bin/print_message
```

Within a bash script, we can set env var without using export, eg:

```sh
#!/usr/bin/env bash

HELLO='world'

echo $HELLO
```

#### Printing Env Vars

We can print an env var using echo, eg: `echo $HELLO`

#### Scoping of Env Vars

When you open up new bash terminals in VSCode, it will not be aware of env vars that you have set in another window.

If you want to persist Env Vars across all future bash terminals that are open, you need to set env vars in your bash profile; eg: `.bash_profile`

#### Persisting Env Vars in GitPod

We can persist env vars into gitpod by storing them in Gitpod Secrets Storage.

```
gp env HELLO='world'
```

All future workspaces launched will set the env vars for all bash terminals open in those workspaces.

You can also set env vars in the `.gitpod.yml` but this can only contain non-sensitive env vars. 

### AWS CLI Installation

AWS CLI is installed for this project via the bash script [`./bin/install_aws_cli`](./bin/install_aws_cli)

[Install or update the latest version of the AWS CLI]https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

[AWS CLI env vars]https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html

We can verify if our AWS credentials are configured correctly by running the following AWS CLI command:
```sh
aws sts get-caller-identity
```

If it's successfull, you should see a JSON payload return like below:

```json
{
    "UserId": "AIDBZB5ZE2TXY33ZI22PP",
    "Account": "123456789012",
    "Arn": "arn:aws:iam::123456789012:user/harshit"
}
```

We'll need to generate the AWS CLI credentials from IAM user in order to use the AWS CLI
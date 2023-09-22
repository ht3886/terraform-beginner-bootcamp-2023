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
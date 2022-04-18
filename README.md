# golang-vagrant-dev-env

## A simple and solid [vagrant](https://www.vagrantup.com/) golang dev environment to build on as your project grows.

`vagrant up`

## What to expect (defaults)

- An Ubuntu (lts), Virtualbox based, Vagrant virtual machine
- 2 CPUS
- 2GB RAM
- Correct version of go installed based on the contents of your projects go.mod file
- Local ip address (automatically assigned via dhcp) for the vm accessible on all ports (ip printed out to terminal on creation of the vm)
- [gosec](https://github.com/securego/gosec) installed globally (simply run `gosec`)
- [staticcheck](https://github.com/dominikh/go-tools) installed globally (simply run `staticcheck`)
- Root of your project inside the vm will be the default: `/vagrant`

## Considerations

- A go mod file containing a version of go must be in the root of the project as this is read to determin the correct version of go to install.
- Remember to treat this as a base for your golang projects with sane defaults and grow the Vagrantfile as necessary with your project.

## Requirements

- Virtualbox

## Contributing

It seams that there are not many up to date golang dev environments on the internet at the moment (they all appear either very opinionated or years old). As such, I will try to keep this one up to date.

If there are any updates you would like to share, or default includes (such as new tools for example), please don't hesitate to open up an issue/pull request.

It's better to air on the side of open and general environment defaults (which can be easily changed and customised by the end user as necessary).

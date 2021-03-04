# Ansible Collection - cub_oit_pe.alertmanager

Large chunks of this were borrowed from the fine work done by the [cloudalchemy group](https://github.com/cloudalchemy/ansible-alertmanager), thanks! Their code uses the MIT license and where applicable I have differentiated their work from ours.

This is a template for developing collections. This template is tightly bound to our specific workflow. As such it is designed to be used on Github with Github actions etc.

## Initial Repository Setup
### Github Workflows
Two workflows are provided by default:
#### release.yml
This action will do the steps required to push a release to Ansible Galaxy, this action is triggered on a push to the 'main' branch. As such if you are in the early stages of development and wish to push directly to main, you should investigate disabling actions, or work in a branch.

This workflow expects `GALAXY_API_KEY` secret to be defined for the repository in Github, this is at current defined organization wide, however, because we do not pay for Github this secret is not available to private repositories.If you are developing using a private repository, make sure you define these secrets for the repository.

#### test-default.yml
This is a template to be used for performing integration and lint testing at the moment. The file is well commented and sections you need to adjust should be obvious. It is recommended that you change the name of this file ass appropriate for you collection and work from there.

This workflow expects a few Github secrets to be defined:
`RHSM_ACTIVATION_KEY`
`RHSM_ORG_ID`
`RHSM_POOL_ID`

Currently these secrets are defined for our Github organization. However, because we do not pay for Github, these organization secrets are not available to private repositories. If you are developing using a private repository, make sure you define these secrets for the repository.

### tests/integration/
There is a default scenario defined in here with the majority of the molecule.yml defined in `tests/integration/basey.yml`. The default configuration is fairly sensible, however you will at a minimum have to modify the `converge.yml` and `verify.yml` files.

## Creating New Roles in the Collection
Please refer the [README](roles/README.md) for roles.

## Local Testing of the Collection
### Integration Testing
Integration testing is handled using [molecule](https://molecule.readthedocs.io/en/latest/) and though docker is supported, podman is preferred for local testing.

#### RHEL Subscription
Because we are heavily based around RHEL we have to work with subscriptions in our testing environment. On Github testing is performed in docker and the UBI container is subscribed after it comes up as part of the `prepare.yml`.

Locally however, if you are using podman, it is expected that the host you are running podman on is subscribed to RHSM. Note that this does not imply that your host is a RHEL host, you can register a Fedora host to RHSM easily. Podman by default exposes the RHSM certificates to the container and as such subscribing is not necessary.

If you are using docker for local testing you will need to export the variables listed [here](#test-default.yml), set `CONTAINER_RT="docker"` and the container should be registered with RHSM after it is brought up.

##### Running Integration Tests
You will want to be located in the `tests/integration/` directory and then run the following:

    integration/ $ molecule -c base.yml -s <scenario name>

Where the scenario name is one of the child directories of `tests/integration`.
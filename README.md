# Ansible Collection - cub_oit_pe.alertmanager

## Description:
This collection installs and configures alertmanager, it is strongly recommended for anyone outside of the team developing this collection NOT to use it. Please instead look to [cloudalchemy's excellent role](https://github.com/cloudalchemy/ansible-alertmanager) for alertmanager.

## Roles in Collection:
There are currently three roles in the collection, however for your average end user you will interact with just one of them, cub_oit_pe.alertmanager.server, the other two are simply in place to provide clean seperation of duties that the server role requires.

The roles are:
- server: Installs and configures an alertmanager server (this is what most users should use).
- install: Does the actual installation of alertmanager.
- configure: Handles the configuration of alertmanager, hevily based on cloudachemy's work.

## Documentation
Documentation for the collection is held in the docs/sources/ directory and is also published as GitHub pages (WIP).

## Licensing
Large chunks of this were borrowed from the fine work done by the [cloudalchemy group](https://github.com/cloudalchemy/ansible-alertmanager), thanks! Their code is licensed under an MIT style license and is copyright:

    Copyright (c) 2017-2018 Pawel Krupa, Roman Demachkovych

    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in all
    copies or substantial portions of the Software.

    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
    SOFTWARE.

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
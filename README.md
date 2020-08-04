
# Genvoy - Clone
<a id="markdown-genvoy---clone" name="genvoy---clone"></a>

An extension for the Genvoy Framework to clone remote repositories.

## Naming
<a id="markdown-naming" name="naming"></a>

genvoy ['jenvoi] is a name combination of both 'Generali' and 'generic' as prefix and 'envoy' as suffix. The word structure describes this solution as a generic approach to transmitting webhook messages (as an envoy) for the Generali.

This word construct only serves the purpose of simplified representation and description of the function of the software. It is not related to similar sounding products from other sectors or product areas and related components.  The function of the software is alternatively described by the longer name "github-webhooks-framework".

The name was changed 07/2020 from "github-webhooks-framework" to "genvoy" because the various functions called by a Webhook call are to be managed as separate repositories.A short name for the framework repository makes it easier to name the function repositories.

The Genvoy Framework can be found here: https://github.com/generaliinformatik/genvoy (alternatively: http://bit.ly/genvoy-framework)

## Purpose
<a id="markdown-purpose" name="purpose"></a>

This extension for the Genvoy framework provides a Python script that can be used to clone a repository in a local directory by event. The script can be used to keep track of the state of the repository as it is modified, thus providing a local copy. This does not prevent destructive changes to a repository, but it does prevent them from having an effect. The backup can then be persisted using an established backup mechanism.

## Table of content
<a id="markdown-table-of-content" name="table-of-content"></a>
<!-- TOC -->

- [Naming](#naming)
- [Purpose](#purpose)
- [Table of content](#table-of-content)
- [Installation](#installation)
- [Configuration](#configuration)
- [Docker](#docker)
- [License](#license)

<!-- /TOC -->

## Installation
<a id="markdown-installation" name="installation"></a>

The following steps are required for commissioning:

1. Clone the Genvoy Framework repository (https://github.com/generaliinformatik/genvoy, alternatively: http://bit.ly/genvoy-framework)
2. Clone the Genvoy clone repository
3. Copy the script `hooks/clone` from the Genvoy clone repository into the `hooks` directory of the Genvoy Framework directory
4. Name the script file in `{event}-clone` (where `{event}` is the event to be monitored, assuming e.g. `push`)
5. Set the execute flag of the script `hooks/push-clone` (via chmod +x)
6. Adjust the settings in the configuration file `clone.json` to your requirements

## Configuration
<a id="markdown-configuration" name="configuration"></a>

The following settings are also included in the `clone.json` and control the backup of the repository:

| Key | Value | Placeholder | Optional | Default |
| --- | --- | :-: | :-: | -- |
| git_url | The URL of the Git Repository to be cloned. This value usually does not need to be adjusted, since it corresponds to the dynamic value of the Git Repository URL.  | &#10003; | - | `{repository/html_url}` |
| clone_dir |  The directory in which the clone is created. In the specified directory, a subdirectory with timestamp is created in which the clone is created. This allows a repository to be saved in any state without overwriting the previous clones. | - |  - | `backup.git` |

## Docker
<a id="markdown-docker" name="docker"></a>

To deploy in a Docker container you may want to persist your cloned repositories. Please map the backup dir to a local dir outside the container:

    docker run --name webhooks \
      -v /path/to/my/clones:/app/backups.git \
      -p 5000:5000 webhooks:latest

## License
<a id="markdown-license" name="license"></a>

APLv2, see [LICENSE](LICENSE)

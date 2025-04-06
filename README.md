# Spec: Development Dockerization v0.0.1

A set of rules for managing the dockerization of services defined in Uqido code-base repositories, with a focus on *reproducibility* and team *autonomy*.

## Dependencies

- https://github.com/Uqido/spec-specification-repository/tree/0.0.1

## Adoption Impact

This specification defines a common repository structure and a basic set of support shell scripts for managing
the dockerization in Uqido repositories—used throughout the development process—in order to:
- Enable developers who are not Docker experts—or who only contribute occasionally—to run the README setup steps autonomously in under 15 minutes, without requiring DevOps support
- Standardize the setup sections of README files, particularly the "Getting Started" instructions, for both development and test environments
- Provide a living documentation point for the development environment the repository is intended to run on
- Simplify and streamline common Docker operations, both locally and in CI environments
- Promote service decoupling and TDD culture by requiring the repository author to provide just two operations—'test' and 'up'—and nothing else

## Normative Content

This specification applies only to Dockerfile's and compose's used during the *development process*.<br>
In order to promote decoupling, developers **should** not store infrastructure related Dockerfile's and compose's in the service repository itself.<br>
Instead, infrastructure-as-code sources **should** be placed in a proper, dedicated infrastructure or orchestration repository.

Repositories adopting this spec **shall** have the following directory structure:

* `<project_root>/`
  * `.dockerignore`
  * `docker/`
    * `compose.test.yml`: the test compose file
    * `compose.development.yml`: the development compose file
    * `bin/`
      * `test.sh`: the shell script executing the test suite, accepting the project test framework parameters (see `dk-test`) 
      * `lint.sh`: the shell script executing the linting suite, accepting the project lint framework parameters (see `dk-lint`) 

This specification includes a set of shell scripts and aliases—located in the `sh_aliases` directory—that provide common Docker operations for building and running repositories that adopt this spec.
These operations cover both basic tasks such as build, up, test, and lint, as well as optional, stack-specific commands for commonly used technologies.<br>
See the sh_aliases README for distribution and usage details.

The project README **shall** have a setup section with instructions to *at least* test, run and lint the code-base.<br>
The instructions **shall** use the sh_aliases whenever technically feasible.<br>
Host mounted volumes created by these instructions **should** contain only files owned by the current user (in particular, not by root).  
The commands `dk-down` and `dk-down-test` **should** result in no running container associated to the development and test environments, respectively.

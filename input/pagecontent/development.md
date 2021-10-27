# Development

Please go through the entire Quick Start narrative.

## Local Development Requirements

Users should have a basic understanding of the command line in their preferred operating system, cURL, git and GitHub.

If prototyping tests, install at least the following:

* **IG Publisher**: See the installation [docs](https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation) which include a Java runtime, Ruby, the Jekyll Ruby gem.

* **Sushi**: See the Sushi installation [docs](https://fshschool.org/docs/sushi/installation/) which include NodeJS.

* **nektos/act**: To run locally, follow the instructions to install [nektos/act]([nektos/act](https://github.com/nektos/act)). The .actrc has been kept in the repository for reference. 

* **Docker and docker-compose**: Act requires docker and docker compose is also required for the tests here. On Windows and macOS, compose is included now in Docker Desktop. Linux users must separately installed docker-compose.

## How to Run Locally

Clone the tests repository.
```
git@github.com:openhie/ddcc-tests.git
cd ddcc-tests
ls -a
```

This testing repository has been specially designed to ensure that all of the tests can run with GitHub Actions on your local computer and can be used to reproduce all results. This is accomplished using [nektos/act](https://github.com/nektos/act).

The `.actrc` file contains an environment variable for `GITHUB_TOKEN`. This is required. It must be available to the CLI environment. If this file is not used, then it must be explicitly passed, e.g. `act -s GITHUB_TOKEN=$GITHUB_TOKEN` or `act -s GITHUB_TOKEN`
<.actrc>
```
--secret GITHUB_TOKEN
--secret-file .secrets
```

`GITHUB_TOKEN` is defined in the shell environment and is required for all but basic operations and for the workflows here to be successful. See [here](https://docs.github.com/en/actions/security-guides/automatic-token-authentication). `.secrets` is illustrates another option some users may find useful to pass variables.

Once nektos/act is installed, the first step is to list the workflows in the repository. It will scan the `.github/workflows` folder.
```
$ act -l
ID                 Stage  Name
build_fsh          0      build_fsh
build_ig           0      build_ig
build              0      build
retrievecert       0      retrievecert
submithealthevent  0      submithealthevent
```

Then jobs can be launched with the `act -j <jobname>` command.
```
$ act -j build_ig
[build_ig/build_ig] 🚀  Start image=catthehacker/ubuntu:act-latest
[build_ig/build_ig]   🐳  docker run image=catthehacker/ubuntu:act-latest platform= entrypoint=["/usr/bin/tail" "-f" "/dev/null"] cmd=[]
[build_ig/build_ig]   🐳  docker exec cmd=[mkdir -m 0777 -p /var/run/act] user=root
[build_ig/build_ig] ⭐  Run Checkout IG
...
```

When act is used, some features of GitHub Actions may not work as expected. This is often because act uses the Docker engine on a platform, and not a full virtual machine as GitHub Actions does. So, some commands, like kubectl, are already included in all GitHub Actions runners but not in act. To address this, act includes an environment variable `env.ACT` which indicates if the workflows are run locally or on the Microsoft Azure VM infrastructure that GitHub uses.

```
# Run this step only if ACT is being used.
- name: Some step
if: ${{ env.ACT }}
# Or, run this step only if ACT is not being used.
if: ${{ !env.ACT }}
```

## Iterating

If you want to run tests against the reference `DDCC:VS Registry Service`, `Repository Service`, and `Generation Service`, clone it and run it.
```
git clone git@github.com:openhie/ddcc-transactions-mediator.git
cd ddcc-transactions-mediator
ls -a
docker-compose -f docker-compose.dev.yml up
```
The server is running the mediator (submit health events) at port 4321, and HAPI is running on 8080. There are tests in the Postman folder to try for the operations.

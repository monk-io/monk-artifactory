JFrog Artifactory meets Monk
===

This repository contains Monk.io template to deploy JFrogs Artifactory system either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

- [JFrog Artifactory meets Monk](#jfrog-artifactory-meets-monk)
  - [Prerequisites](#prerequisites)
    - [Make sure monkd is running.](#make-sure-monkd-is-running)
    - [Clone Repository](#clone-repository)
    - [Load Template](#load-template)
    - [Verify if it's loaded correctly](#verify-if-its-loaded-correctly)
  - [Deploy Stack](#deploy-stack)
    - [Deploy Artifactory server](#deploy-artifactory-server)
  - [Stop, remove and clean up workloads and templates](#stop-remove-and-clean-up-workloads-and-templates)
  - [Persistency](#persistency)

## Prerequisites
- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

### Make sure monkd is running.

```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

### Clone Repository

```bash
git clone git@github.com:monk-io/monk-artifactory.git
```

### Load Template

```bash
cd monk-artifactory
monk load manifest.yaml
```

### Verify if it's loaded correctly

```bash
$ monk list -l jfrog

✔ Got the list
Type      Template        Repository  Version  Tags
runnable  jfrog/artifactory  local       -        -
```

## Deploy Stack

### Deploy Artifactory server

```bash
$ monk run jfrog/artifactory
✔ Starting the job: local/jfrog/artifactory... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% docker.bintray.io/jfrog/artifactory-oss:latest local
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ Started local/jfrog/artifactory

🔩 templates/local/jfrog/artifactory
 └─🧊 Peer local
    └─🔩 templates/local/jfrog/artifactory
       └─📦 67c82920a8786434a24b6aad3e35bb95--jfrog-artifactory-artifactory
          ├─🧩 docker.bintray.io/jfrog/artifactory-oss:latest
          ├─💾 /var/lib/monkd/volumes/jfrog/artifactory -> /var/opt/jfrog/artifactory
          ├─🔌 open 1.1.1.1:8082 -> 8082
          └─🔌 open 1.1.1.1:8081 -> 8081

💡 You can inspect and manage your above stack with these commands:
        monk logs (-f) local/jfrog/artifactory - Inspect logs
        monk shell     local/jfrog/artifactory - Connect to the container's shell
        monk do        local/jfrog/artifactory/action_name - Run defined action (if exists)
💡 Check monk help for more!
```


## Stop, remove and clean up workloads and templates

```bash
monk purge    jfrog/artifactory
monk purge -x jfrog/artifactory
```

## Persistency
If you're using any of the clouds available via Monk. You can use volume definition to spin a disk block device to make your Artifactory instance independent from the node it's running on.
To do simply uncomment the `volume` block in `manifest.yaml`

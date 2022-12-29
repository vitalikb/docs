---
title: Configuraation
description: Docs intro
layout: ../../layouts/MainLayout.astro
mascot: Hello
---

Kubeshark reads configuration elements both from the CLI and from a configuration file that can be located either in `$HOME/.kubeshark/config.yaml` or at a diffrent location speciied as a CLI flag: `--configpath string`.


## The Config Command

The `config` command generates Kubeshark config file with default values.

```shell
Usage:
  kubeshark config [flags]

Flags:
  -h, --help         help for config
  -r, --regenerate   Regenerate the config file with default values to path $HOME/.kubeshark/config.yaml or to chosen path using --configpath

Global Flags:
      --configpath string   Override config file path using --configpath (default "$HOME/.kubeshark/config.yaml")
  -d, --debug               Enable debug mode.
      --set strings         Override values using --set
```

## Popular Configuration Elements

#### Private Docker Registry

Use when you'd like Kubeshark to pull it's images from a local Docker respository. This is useful in an Enterprise envrionment, where images are built  and hosted locally.

```shell
tap:
    docker:
        registry: docker.io/kubeshark
        tag: latest
        imagepullpolicy: Always
```

CLI Alternative: `-r, --docker-registry string       The Docker registry that's hosting the images. (default "docker.io/kubeshark")`

### Web UI IP and Accessibility

For security reasons, the default address of the proxy host for the Web UI is set to 127.0.0.1 that allows opening only local connections.

```shell
tap:
    proxy:
        host: 127.0.0.1
```

Consider changing this address to 0.0.0.0 or any other publically accessible IP, to allow public address. Keep in mind that WebUI access isn't encrypted or authenticated.


### Worker Storage Limit

Kubeshark **Workers** store the captured traffic locally at the Node level with no limit other than the limit of the volumes attached to the Nodes.

```shell
tap:
    max-entries-db-size: 200MB
```


### Kubeshark Resource Assignment Limits

Use to change the amount of resources assigned to Kubeshark.

```shell
tap:
    resources:
        worker:
            cpu-limit: 750m
            memory-limit: 1Gi
            cpu-requests: 50m
            memory-requests: 50Mi
        hub:
            cpu-limit: 750m
            memory-limit: 1Gi
            cpu-requests: 50m
            memory-requests: 50Mi
```

### Run Kubeshark Headless

By default, Kubeshark opens the Web UI. If you are running Kubeshark on a headless machine and you'd like NOT to open the Web UI, set `headless` to true.

```shell
headless: false
```

### Public IP and Headless

This is a very popular option that enables running Kubeshark on a puvlic IP and without opening the Web UI.

```shell
tap:
    proxy:
        host: 0.0.0.0
headless: true
```

Now you can use web browser to view Kubeshark running on a remote server.

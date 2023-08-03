# agent-k8s-spinplug-releases

Repository for Armory's Agent K8s plugin releases

## About

The Armory Scale Agent for Spinnaker and Kubernetes is a lightweight, scalable service that monitors your Kubernetes infrastructure and streams changes back to Spinnaker’s Clouddriver service.

https://docs.armory.io/scale-agent/

A more efficient way to deploy to Kubernetes

- Don't run agents to cache: list & watch
- Don't run kubectl and all its cache: use Kubernetes APIs
- Don't struggle with credentials: read them from `SpinnakerAccount`s

## Installation & Configuration

_It should be noted that the plugins framework for Spinnaker is still in active development so installation instructions may change_.

1. Identify the released version of the plugin you wish to install. Official releases are found [here](https://docs.armory.io/scale-agent/release-notes/agent-plugin/).
2. In your Spinnaker configuration, add the following repository & plugin configuration.

    ```yaml
    spinnaker:
      extensibility:
        repositories:
          armory-agent-plugin:
            url: https://raw.githubusercontent.com/armory-io/agent-k8s-spinplug-releases/master/repositories.json
          armory-agent-plugin-rc:
            url: https://raw.githubusercontent.com/armory-io/agent-k8s-spinplug-releases/master/rc/repositories-rc.json
        plugins:
          Armory.Kubesvc:
            enabled: true
            version: 0.9.74
            extensions:
              armory.kubesvc:
                enabled: true

    # This portion is required in Clouddriver profile
    kubesvc:
      cluster: kubernetes
      dynamicAccounts:
        enabled: true

    ```

    The above configuration also assumes that you've installed or deployed golang Agent K8s [found here](https://docs.armory.io/scale-agent/install/install-agent-service-kubectl/)

3. On startup, the plugin will be downloaded and installed to Clouddriver


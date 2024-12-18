---
title: "Oracle Backend for Microservices and AI IntelliJ Plugin"
description: "IntelliJ Plugin for Oracle Backend for Microservices and AI"
keywords: "intellij plugin ide springboot spring development microservices development oracle backend"
---

## GA 1.3.1 - October, 2024

General updates.

## GA 1.3.0 - September, 2024

Oracle Backend for Microservices and AI (OBaaS) is an IntelliJ plugin to browse, deploy, and modify workloads on the Oracle Backend for Microservices and AI platform.This plug-in implements the functionalities available in the [Oracle Backend for Microservices and AI CLI](../../development/cli), simplifying  access to Oracle Backend for Microservices and AI deployments from an IntelliJ IDE. 

The plug-in allows access to the Oracle Backend for Microservices and AI platform services, including the Grafana, Spring, APISIX, Eureka and Jaeger web admin consoles. Additionally, you may create and bind workloads to your  Oracle Backend for Microservices and AI database deployment. Users may inspect Oracle Backend for Microservices and AI deployment namespaces, workloads, and related configuration.

See the Oracle Free Use Terms and Conditions [License](https://oss.oracle.com/licenses/upl/)

## Prerequisites

* An operational Oracle Backend for Microservices and AI deployment, as configured through platform [setup](../../setup/).
* Access to a Kubernetes cluster where Oracle Backend for Microservices and AI is deployed from your IntelliJ IDE.

## Installation

1. Download the IntelliJ plugin ZIP file from [here](https://github.com/oracle/microservices-datadriven/releases/tag/OBAAS-1.3.1).

2. On the IntelliJ Settings plugins page, click the "gear" icon and select **Install Plugin from Disk...**. Browse your filesystem for the IntelliJ plugin ZIP file, and select it.

    ![plugin-intell](./images/install-from-disk.png)

3. Click **OK**, and restart your IDE to load the Oracle Backend for Microservices and AI plugin.

4. If you do not see the Oracle Backend for Microservices and AI icon on your IDE's toolbar, navigate to View -> Tool Windows, and select "OBaaS" to add it to your IDE's tool window bar.

### Proxy Configuration

If you are connecting to your Kubernetes cluster through a proxy server, configure your IntelliJ proxy settings from Settings -> Proxy. Th Oracle Backend for Microservices and AI will use your IntelliJ system proxy settings to connect to your Kubernetes cluster.

## Configuring the Oracle Backend for Microservices and AI Connection

1. Open the plugin tool window by clicking the "OBaaS" icon on the IntelliJ tool bar, and click the "wrench" icon to open the Oracle Backend for Microservices and AI connection settings.

    ![open-settings](./images/open-settings.png)

2. Enter the Oracle Backend for Microservices and AI username, password, kubeconfig for the Kubernetes cluster, and the local port the Oracle Backend for Microservices and AI admin tunnel will bind to. The default kubeconfig and context may already be selected.

   ![plugin-settings](./images/settings.png)

3. When you're done, click "Test Connection" to verify the Oracle Backend for Microservices and AI connectivity. If you've configured your kubeconfig and Oracle Backend for Microservices and AI credentials correctly, you should see a connection successful message:

    ![test-connection](./images/test-connection.png)

### Known issue with Kubernetes authentication

If you are using a Kubeconfig shell exec config to authenticate to your Kubernetes cluster from the Oracle Backend for Microservices and AI, you may need to provide the full path to the authenticating binary:

```yaml
users:
- name: my-user
  user:
    exec:
      apiVersion: client.authentication.k8s.io/v1beta1
       # Provide the full path to the authenticating binary here
      command: /usr/local/bin/oci
```

### Managing Oracle Backend for Microservices and AI Connection States

To refresh the Oracle Backend for Microservices and AI connection, click the "Refresh" button at the top of the Oracle Backend for Microservices and AI tool window.

To cancel all active connections, click the red "Close Connections" button at the top of the Oracle Backend for Microservices and AI tool window.

## Explore Oracle Backend for Microservices and AI Resources

Once you are connected to Oracle Backend for Microservices and AI, click on the context node in the tool window tree to view Oracle Backend for Microservices and AI resources in your cluster.

- Oracle Backend for Microservices and AI namespaces are shown in the "namespaces" section, each namespace containing a list of applications.
- Links to platform service dashboards are shown in the "platform services" section.
- Configuration properties are listed in the "configuration" section.

![explore-resources](./images/explore-resources.png)

## Working with namespaces and workloads
   
### Create a new namespace

To create a new namespace, right click on the namespace and select "Add Namespace". 

![add-namespace](./images/add-namespace.png)

After you click OK, the namespace will be created and appear in the namespace list in a few moments.

![namespace-created](./images/namespace-created.png)

You can delete a namespace by right clicking on that namespace, and selecting "Delete Namespace". When a namespace is deleted, all applications in the namespace will also be deleted.

### Deploying workloads into namespaces

To deploy a workload into a namespace, right click that namespace and select "Add Workload -> Upload .jar" for JVM workloads or "Add Workload -> Upload .exec" for GraalVM native workloads.

On the Add Workload form, enter workload data.
- Database username will default to the workload name if not specified, and is used for Java Message Service Transactional Event Queue authentication.

![upload-jar](./images/upload-jar.png)

When you click OK, the JAR/exec file will be uploaded to Oracle Backend for Microservices and AI, an image is built, and the workload deployed to the cluster namespace. The task duration will vary depending on the size of the upload file and your network connection for upload.

### Workload autoscalers

To create an autoscaler for a workload, right-click the workload and select "Create Autoscaler". Autoscalers are configured on workload CPU, and specify minimum and maximum scale replicas.

![create-autoscaler](./images/create-autoscaler.png)

You may also deletea workload's autoscaler from the workload context menu.

### Publishing workloads

A workload can be published on an APISIX route by right-clicking the workload, providing the APISIX admin key and the desired route.

![publish-workload](./images/publish-workload.png)

## Accessing Oracle Backend for Microservices and AI Platform Services

To access the web console of an Oracle Backend for Microservices and AI platform service (Grafana, Spring Admin, APISIX, Eureka, or Jaeger), right-click on the service's name under the "platform services" section and click "Connect".

![platform-services](./images/platform-services.png)

Once the connection is complete, click the "Open console" link on the completion message to navigate to the service's web console.

![grafana-connect](./images/grafana-connect.png)

## Configuration Properties

Workload configuration can be browsed and edited through the "configuration" section. To add a new configuration property, right-click either the top-level configuration section or a specific configuration node.

A property is associated with a given configuration service, and may have a label, profile, key, and value.

---
title: "Deploying jobs in production environments"
excerpt: "Find out how to deploy your advanced flows in a Flink cluster as part of your production environment."
categories: advanced
slug: deploying-production
toc: true
---

Find out how to deploy your advanced flows in a Flink cluster as part of your production environment.

**Important:** This deployment cannot be used with {{site.data.reuse.ep_name}} UI.

**Note:** The [Apache operator sample](https://github.com/apache/flink-kubernetes-operator/tree/main/examples/flink-sql-runner-example){:target="_blank"} that is referenced in the following sections points to the version of the sample in the `main` branch, which is up to date, and might include fixes that are absent in the `release-1.5` and `release-1.6` branches.

## Prerequisites

- The SQL statements are exported from the {{site.data.reuse.ep_name}} UI and saved to a file, for example, `statements.sql`.

  For more information, see [Exporting flows](../exporting-flows).

- You adequately updated the Flink SQL Kafka connectors properties and values defined in file `statements.sql` to match your target environment:

   - Sensitive credentials.

     For security reasons, the values containing sensitive credentials are removed from the {{site.data.reuse.ep_name}} UI when exporting the SQL statements, so you must restore them.

     For more information about Flink SQL Kafka connectors, see the [Flink documentation](https://nightlies.apache.org/flink/flink-docs-release-1.17/docs/connectors/table/kafka/){:target="_blank"}.

   - Connector properties values.

     For more information about how events can be consumed from Kafka topics, see the [Flink documentation](https://nightlies.apache.org/flink/flink-docs-release-1.17/docs/connectors/table/kafka/#start-reading-position){:target="_blank"}.

     **Note:** The Kafka [connector](https://nightlies.apache.org/flink/flink-docs-release-1.17/docs/connectors/table/kafka/#connector){:target="_blank"} value must be `kafka`.

   - To deploy a running Flink job, the SQL statements in file `statements.sql` must contain one of the following:
      - A definition of a Flink SQL Kafka sink (also known as event destination), and an `INSERT INTO` clause that selects the columns of the last temporary view into this sink.
      - A `SELECT` clause that takes one or all of the columns of the last temporary view.

     For more information about how to define a Flink SQL sink, see the [Flink documentation](https://nightlies.apache.org/flink/flink-docs-release-1.17/docs/dev/table/sql/insert/#insert-from-select-queries){:target="_blank"}.

## Setup a connection to the Flink cluster

1. {{site.data.reuse.openshift_cli_login}}


2. Switch to the namespace where the {{site.data.reuse.flink_long}} is installed:

   ```shell
   oc project <namespace>
   ```

## Build and deploy a Flink SQL runner

You can use a Kubernetes `FlinkDeployment` custom resource in application mode to deploy a Flink job for processing and deploying the statements in the file `statements.sql`.

A sample application [flink-sql-runner-example](https://github.com/apache/flink-kubernetes-operator/tree/main/examples/flink-sql-runner-example){:target="_blank"} is provided in the Apache Flink GitHub repository for that purpose.

Follow the [instructions](https://github.com/apache/flink-kubernetes-operator/tree/main/examples/flink-sql-runner-example#usage){:target="_blank"} to build:
- the flink-sql-runner-example JAR file (Flink job)
- the Docker image

Some adaptations to this procedure are required to build the Docker image and use the file `statements.sql`:

1. Modify the [Dockerfile](https://github.com/apache/flink-kubernetes-operator/blob/main/examples/flink-sql-runner-example/Dockerfile){:target="_blank"} to use the IBM Flink image:

   a. Execute the following command to extract the Flink image name including its SHA digest from the `ClusterServiceVersion` (CSV).

   ```sql
   oc get csv -o jsonpath='{.spec.install.spec.deployments[*].spec.template.spec.containers[0].env[?(@.name=="IBM_FLINK_IMAGE_V1_0_1")].value}' ibm-eventautomation-flink.v1.0.1
   ```

   b. Edit the [Dockerfile](https://github.com/apache/flink-kubernetes-operator/blob/main/examples/flink-sql-runner-example/Dockerfile){:target="_blank"} and change the `FROM` clause to IBM Flink image with its SHA digest, as determined in the previous step.

   ```shell
   FROM <IBM Flink image with digest>
   ```

   c. Remove the sample SQL statement files from the directory [sql-scripts](https://github.com/apache/flink-kubernetes-operator/tree/main/examples/flink-sql-runner-example/sql-scripts){:target="_blank"}.

   d. Copy the file `statements.sql` to the directory [sql-scripts](https://github.com/apache/flink-kubernetes-operator/tree/main/examples/flink-sql-runner-example/sql-scripts){:target="_blank"}.

   e. [Build the docker image](https://github.com/apache/flink-kubernetes-operator/blob/main/examples/flink-sql-runner-example/README.md#usage){:target="_blank"} and push it to a registry accessible from your {{site.data.reuse.openshift_short}}. If your registry requires authentication, configure the image pull secret, for example, by using the [global cluster pull secret](https://docs.openshift.com/container-platform/4.12/openshift_images/managing_images/using-image-pull-secrets.html#images-update-global-pull-secret_using-image-pull-secrets){:target="_blank"}.

2. Create the {{site.data.reuse.flink_long}} `FlinkDeployment` custom resource.

   a. Choose the [Production - Flink Application cluster](../../installing/planning/#flink-production-application-cluster-sample) sample, or a production sample with persistent storage in the {{site.data.reuse.openshift_short}} OperatorHub. If you prefer to not use a provided sample, add the following parameter to set a timeout period for event sources when they are marked idle. This allows downstream tasks to advance their watermark. Idleness is not detected by default. The parameter is included in all the provided samples.

   ```yaml
   spec:
     flinkConfiguration:
       table.exec.source.idle-timeout: '30 s'
   ```
  
   For more information about `table.exec.source.idle-timeout`, see the [Flink documentation](https://nightlies.apache.org/flink/flink-docs-release-1.17/docs/dev/table/config/#table-exec-source-idle-timeout){:target="_blank"}.

   b. Append the following `spec.job` parameter, or edit the existing parameter if using the Production - Flink Application cluster sample:

   ```yaml
   spec:
     job:
       jarURI: local:///opt/flink/usrlib/sql-runner.jar
       args: ["/opt/flink/usrlib/sql-scripts/statements.sql"]
       parallelism: 1
       state: running
       upgradeMode: savepoint
   ```

   c. Set the Flink image:
   ```yaml
   spec:
     image: <image built at step 1.e>
   ```

3. Deploy this `FlinkDeployment` custom resource.


## Changing the parallelism of a Flink SQL runner

<!-- hide autoscaler
#### Using explicit configuration
hide autoscaler -->

1. Edit the `FlinkDeployment` custom resource.

   a. Ensure that the Flink cluster has enough task slots to fulfill the targeted parallelism value.

   ```shell
   Task slots = spec.taskmanager.replicas × spec.flinkConfiguration["taskmanager.numberOfTaskSlots"] 
   ```

   **Note:** In case there are not enough free task slots when the Flink job is redeployed with the targeted job parallelism value,
   no additional `TaskManager` will be created even with `spec.job.mode` set to `native`.

   b. Change the `spec.job.parallelism` value, then set `spec.job.state` to `running` and `spec.job.upgradeMode` to `savepoint`.

   ```yaml
   spec:
     job:
       jarURI: local:///opt/flink/usrlib/sql-runner.jar
       args: ["/opt/flink/usrlib/sql-scripts/statements.sql"]
       parallelism: 2
       state: running
       upgradeMode: savepoint
   ```

2. Apply the modified `FlinkDeployment` custom resource.

   The following operations are automatically performed by Flink:
   - A savepoint is created before the Flink job is suspended.
   - The Flink cluster is shutdown, the `JobManager` and `TaskManager` pods are terminated.
   - A Flink cluster is created with new `JobManager` and `TaskManager` pods.
   - The Flink job is restarted from the savepoint.

<!-- hide autoscaler
#### Using the Flink autoscaler

1. Ensure that the Kafka topics for the sources and the destination are defined with more than one partition.

2. Edit the `FlinkDeployment` custom resource.

   a. Ensure that `spec.job.parallelism` option is not set and `spec.job.upgradeMode` value is set to `savepoint`.

   ```yaml
   spec:
     job:
       jarURI: local:///opt/flink/usrlib/sql-runner.jar
       args: ["/opt/flink/usrlib/sql-scripts/statements.sql"]
       state: running
       upgradeMode: savepoint
   ```

    b. In the `spec.flinkConfiguration`, add the Flink autoscaler parameters to match your workload expectations.

      For more information about the autoscaler and a basic configuration example, see [Flink autoscaler](https://nightlies.apache.org/flink/flink-kubernetes-operator-docs-release-1.5/docs/custom-resource/autoscaler/)

      For a detailed configuration reference, see the [Flink autoscaler configuration options](https://nightlies.apache.org/flink/flink-kubernetes-operator-docs-release-1.5/docs/operations/configuration/#autoscaler-configuration)

      **Important:** If you have already defined the `pipeline.max-parallelism` option in `spec.flinkConfiguration` then do not alter the value.
     This would result in an incompatible change when the Job is restarted from an existing savepoint.

3. Apply the modified `FlinkDeployment` custom resource.
hide autoscaler -->

## Trigger a savepoint for a running Flink SQL job

1. Edit the `FlinkDeployment` custom resource.

2. Make the following modifications

   a. Ensure that the value of `spec.job.upgradeMode` is `savepoint`.

   b. Ensure that the value of `spec.job.state` is `running`.

   c. Ensure that the value of `spec.job.savepointTriggerNonce` is an integer that has never been used before for that option.

   ```yaml
   spec:
     job:
       jarURI: local:///opt/flink/usrlib/sql-runner.jar
       args: ["/opt/flink/usrlib/sql-scripts/statements.sql"]
       savepointTriggerNonce: <integer value>
       state: running
       upgradeMode: savepoint
   ```

3. Apply the modified `FlinkDeployment` custom resource.

   A new savepoint is created in the directory specified in `spec.flinkConfiguration["state.savepoints.dir"]`.

## Stop a Flink SQL with a savepoint

1. Edit the `FlinkDeployment` custom resource.

2. Make the following modifications

   a. Ensure that the value of `spec.job.upgradeMode` is `savepoint`.

   b. Ensure that the value of `spec.job.state` is `suspended` to stop the Flink job.

   ```yaml
   spec:
     job:
       jarURI: local:///opt/flink/usrlib/sql-runner.jar
       args: ["/opt/flink/usrlib/sql-scripts/statements.sql"]
       state: suspended
       upgradeMode: savepoint
   ```

3. Apply the modified `FlinkDeployment` custom resource.

   A new savepoint is created in the directory specified in `spec.flinkConfiguration["state.savepoints.dir"]`.

## Resume a Flink SQL with a savepoint

1. Edit the `FlinkDeployment` custom resource.

2. Make the following modifications:

   a. Ensure that the value of `spec.job.upgradeMode` is `savepoint`.

   b. Ensure that the value of `spec.job.state` is `running` to resume the Flink job.

   c. Ensure that the same directory is set for the parameters `spec.job.initialSavepointPath` and `spec.flinkConfiguration["state.savepoints.dir"]`.

   ```yaml
   spec:
     job:
       jarURI: local:///opt/flink/usrlib/sql-runner.jar
       args: ["/opt/flink/usrlib/sql-scripts/statements.sql"]
       state: running
       upgradeMode: savepoint
       initialSavepointPath: <savepoint directory>
       allowNonRestoredState: true
   ```

3. Apply the modified `FlinkDeployment` custom resource.

   The Flink job is automatically resumed from the latest savepoint that Flink finds in `spec.job.initialSavepointPath`.
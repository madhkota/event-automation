---
title: "Support matrix"
description: "Find out about capability versions, supported platforms, and other support information, including compatibility."
permalink: /support/matrix/
toc: true
section: "IBM Event Automation support"
cardType: "large"
order: 1
layout: pagesInsideCollection
---

## {{site.data.reuse.es_name}}

See the following table for information about the latest {{site.data.reuse.es_name}} versions. For information about earlier versions, see the [earlier version tables]({{ 'support/matrix/es-earlier/' | relative_url }}).

**Note:** Product defect fixes and security updates are only available in the latest CD version, in line with the IBM's continuous delivery lifecycle policy (for more information, see the {{site.data.reuse.es_name}} [support lifecycle addendum](https://www.ibm.com/support/pages/node/6589953){:target="_blank"}). Ensure you stay current with the installation of the latest CD update packages.

**Important:** If you want to set up [persistent storage]({{'es' | relative_url}}/installing/planning/#planning-for-persistent-storage), {{site.data.reuse.es_name}} requires block storage configured to use the XFS or ext4 file system. The use of file storage (for example, NFS) is not recommended. <br> For example, you can use one of the following systems:
- [Kubernetes local volumes](https://kubernetes.io/docs/concepts/storage/volumes/#local){:target="_blank"}
- [Amazon Elastic Block Store (EBS)](https://kubernetes.io/docs/concepts/storage/volumes/#awselasticblockstore){:target="_blank"}
- [Rook Ceph](https://rook.io/docs/rook/v1.3/ceph-storage.html){:target="_blank"} 
- [Red Hat OpenShift Container Storage](https://docs.openshift.com/container-platform/4.6/storage/persistent_storage/persistent-storage-ocs.html){:target="_blank"}

{{site.data.reuse.es_name}} version | Operator version | Operator channel | Kafka version shipped | CASE version | Container platform  | Systems | 
-----------------------------------------------|------------------|------------------|-----------------------|---------------------|---------|
11.2.3  | 3.2.3  | v3.2  | 3.5.1  | 3.2.3 | {{site.data.reuse.openshift}} versions 4.10 to 4.12, all fix levels (see [support dates](https://access.redhat.com/support/policy/updates/openshift#dates){:target="_blank"}).<br> <br> Managed OpenShift services on cloud platforms (PaaS): <br>- Red Hat OpenShift on IBM Cloud <br> - Azure Red Hat OpenShift <br> - Red Hat OpenShift Service on AWS <br> <br> **Note:** [AWS ECS Fargate](https://aws.amazon.com/fargate/){:target="_blank"} is not supported. <br> <br> OpenShift on cloud infrastructure (IaaS): <br> - IBM Cloud <br> - Microsoft Azure <br> - Amazon Web Services <br> <br> Kubernetes platforms that support the Red Hat Universal Base Images (UBI) containers, versions 1.21 to 1.27  | - Linux on IBM Power Systems (ppc64le) <br> - Linux 64-bit (x86_64) systems <br> - Linux on IBM z13 (s390x) or later systems |
11.2.2  | 3.2.2  | v3.2  | 3.4.0  | 3.2.2 | {{site.data.reuse.openshift}} versions 4.10 to 4.12, all fix levels (see [support dates](https://access.redhat.com/support/policy/updates/openshift#dates){:target="_blank"}).<br> <br> Managed OpenShift services on cloud platforms (PaaS): <br>- Red Hat OpenShift on IBM Cloud <br> - Azure Red Hat OpenShift <br> - Red Hat OpenShift Service on AWS <br> <br> **Note:** [AWS ECS Fargate](https://aws.amazon.com/fargate/){:target="_blank"} is not supported. <br> <br> OpenShift on cloud infrastructure (IaaS): <br> - IBM Cloud <br> - Microsoft Azure <br> - Amazon Web Services <br> <br> Kubernetes platforms that support the Red Hat Universal Base Images (UBI) containers, versions 1.21 to 1.27  | - Linux on IBM Power Systems (ppc64le) <br> - Linux 64-bit (x86_64) systems <br> - Linux on IBM z13 (s390x) or later systems |
11.2.1  | 3.2.1  | v3.2  | 3.4.0  | 3.2.1 | {{site.data.reuse.openshift}} versions 4.10 to 4.12, all fix levels (see [support dates](https://access.redhat.com/support/policy/updates/openshift#dates){:target="_blank"}).<br> <br> Managed OpenShift services on cloud platforms (PaaS): <br>- Red Hat OpenShift on IBM Cloud <br> - Azure Red Hat OpenShift <br> - Red Hat OpenShift Service on AWS <br> <br> **Note:** [AWS ECS Fargate](https://aws.amazon.com/fargate/){:target="_blank"} is not supported. <br> <br> OpenShift on cloud infrastructure (IaaS): <br> - IBM Cloud <br> - Microsoft Azure <br> - Amazon Web Services <br> <br> Kubernetes platforms that support the Red Hat Universal Base Images (UBI) containers, versions 1.21 to 1.27  | - Linux on IBM Power Systems (ppc64le) <br> - Linux 64-bit (x86_64) systems <br> - Linux on IBM z13 (s390x) or later systems |
11.2.0  | 3.2.0  | v3.2  | 3.4.0  | 3.2.0 | {{site.data.reuse.openshift}} versions 4.10 to 4.12, all fix levels (see [support dates](https://access.redhat.com/support/policy/updates/openshift#dates){:target="_blank"}).<br> <br> Managed OpenShift services on cloud platforms (PaaS): <br>- Red Hat OpenShift on IBM Cloud <br> - Azure Red Hat OpenShift <br> - Red Hat OpenShift Service on AWS <br> <br> **Note:** [AWS ECS Fargate](https://aws.amazon.com/fargate/){:target="_blank"} is not supported. <br> <br> OpenShift on cloud infrastructure (IaaS): <br> - IBM Cloud <br> - Microsoft Azure <br> - Amazon Web Services <br> <br> Kubernetes platforms that support the Red Hat Universal Base Images (UBI) containers, versions 1.21 to 1.26  | - Linux on IBM Power Systems (ppc64le) <br> - Linux 64-bit (x86_64) systems <br> - Linux on IBM z13 (s390x) or later systems |
11.1.6  | 3.1.6  | v3.1  | 3.4.0  | 1.7.6  | {{site.data.reuse.openshift}} versions 4.8 to 4.12, all fix levels (see [support dates](https://access.redhat.com/support/policy/updates/openshift#dates){:target="_blank"}). <br> <br> Managed OpenShift services on cloud platforms (PaaS): <br>- Red Hat OpenShift on IBM Cloud <br> - Azure Red Hat OpenShift <br> - Red Hat OpenShift Service on AWS <br> <br> OpenShift on cloud infrastructure (IaaS): <br> - IBM Cloud <br> - Microsoft Azure <br> - Amazon Web Services <br> <br> | - Linux on IBM Power Systems (ppc64le) <br> - Linux 64-bit (x86_64) systems <br> - Linux on IBM z13 (s390x) or later systems |


## {{site.data.reuse.eem_name}}

**Note:** If you want to set up [persistent storage]({{'eem' | relative_url}}/installing/planning/#planning-for-persistent-storage), {{site.data.reuse.eem_name}} requires persistent volumes with the following capabilities: `volumeMode: Filesystem` and `accessMode: ReadWriteOnce`. For example, you can use Rook Ceph. For details, see [Storage requirements for {{site.data.reuse.eem_name}}]({{'eem' | relative_url}}/installing/prerequisites/#data-storage-requirements).

{{site.data.reuse.eem_name}} version | Operator version | Operator channel | CASE version | Container platform  | Systems | 
-----------------------------------------------|------------------|------------------|-----------------------|---------------------|---------|
11.0.3  | 11.0.3  | v11.0  | 11.0.3 | {{site.data.reuse.openshift}} versions 4.10 to 4.12, all fix levels (see [support dates](https://access.redhat.com/support/policy/updates/openshift#dates){:target="_blank"}). <br> <br> Managed OpenShift services on cloud platforms (PaaS): <br>- Red Hat OpenShift on IBM Cloud <br> - Azure Red Hat OpenShift <br> - Red Hat OpenShift Service on AWS <br> <br> **Note:** [AWS ECS Fargate](https://aws.amazon.com/fargate/){:target="_blank"} is not supported. <br> <br> OpenShift on cloud infrastructure (IaaS): <br> - IBM Cloud <br> - Microsoft Azure <br> - Amazon Web Services  | - Linux 64-bit (x86_64) systems | 
11.0.2  | 11.0.2  | v11.0  | 11.0.2 | &nbsp;  | &nbsp; |
11.0.1  | 11.0.1  | v11.0  | 11.0.1 | &nbsp;  | &nbsp; |
11.0.0  | 11.0.0  | v11.0  | 11.0.0 | &nbsp;  | &nbsp; |


## {{site.data.reuse.ep_name}}

**Note:** If you want to set up [persistent storage]({{'ep' | relative_url}}/installing/planning/#planning-for-persistent-storage), {{site.data.reuse.ep_name}} requires persistent volumes with the following capabilities: `volumeMode: Filesystem` and `accessMode: ReadWriteOnce`. For example, you can use Rook Ceph. For details, see [Storage requirements for {{site.data.reuse.ep_name}}]({{'ep' | relative_url}}/installing/prerequisites/#storage-requirements-for-event-processing).

{{site.data.reuse.ep_name}} version | Operator version | Operator channel | CASE version | Container platform  | Systems |
-----------------------------------------------|--------|------------------|--------|---------------------|---------|
1.0.3  | 1.0.3  | v1.0  | 1.0.3  | {{site.data.reuse.openshift}} versions 4.10 to 4.12, all fix levels (see [support dates](https://access.redhat.com/support/policy/updates/openshift#dates){:target="_blank"}). <br> <br> Managed OpenShift services on cloud platforms (PaaS): <br>- Red Hat OpenShift on IBM Cloud <br> - Azure Red Hat OpenShift <br> - Red Hat OpenShift Service on AWS <br> <br> **Note:** [AWS ECS Fargate](https://aws.amazon.com/fargate/){:target="_blank"} is not supported. <br> <br> OpenShift on cloud infrastructure (IaaS): <br> - IBM Cloud <br> - Microsoft Azure <br> - Amazon Web Services  | - Linux 64-bit (x86_64) systems |
1.0.2  | 1.0.2  | v1.0  | 1.0.2  | &nbsp;  | &nbsp; |
1.0.1  | 1.0.1  | v1.0  | 1.0.1  | &nbsp;  | &nbsp; |
1.0.0  | 1.0.0  | v1.0  | 1.0.0  | &nbsp;  | &nbsp; | 


**Note:** If you want to set up [persistent storage]({{'ep' | relative_url}}/installing/planning/#planning-for-persistent-storage), {{site.data.reuse.flink_long}} requires persistent volumes with the following capabilities: `volumeMode: Filesystem` and `accessMode: ReadWriteMany`. For example, you can use Rook Ceph. For details, see [Storage requirements for Flink]({{'ep' | relative_url}}/installing/prerequisites/#storage-requirements-for-flink).

Flink version | {{site.data.reuse.flink_long}} version | Operator channel | CASE version | Container platform  | Systems |
-----------------------------------------------|--------|------------------|--------------|---------------------|---------|
1.17.1  | 1.0.2  | v1.0  | 1.0.2 | {{site.data.reuse.openshift}} versions 4.10 to 4.12, all fix levels (see [support dates](https://access.redhat.com/support/policy/updates/openshift#dates){:target="_blank"}). <br> <br> Managed OpenShift services on cloud platforms (PaaS): <br>- Red Hat OpenShift on IBM Cloud <br> - Azure Red Hat OpenShift <br> - Red Hat OpenShift Service on AWS <br> <br> **Note:** [AWS ECS Fargate](https://aws.amazon.com/fargate/){:target="_blank"} is not supported. <br> <br> OpenShift on cloud infrastructure (IaaS): <br> - IBM Cloud <br> - Microsoft Azure <br> - Amazon Web Services  | Linux 64-bit (x86_64) systems |
1.17.1  | 1.0.1  | v1.0  | 1.0.1 |
1.17.0  | 1.0.0  | v1.0  | 1.0.0 |
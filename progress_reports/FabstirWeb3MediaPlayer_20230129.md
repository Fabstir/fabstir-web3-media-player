
# Fabstir Web3 Media Player - Progress Report (Jan 2023)

By Jules Lai

  

This progress report highlights largely preparation work for the architecture of **Fabstir Web3 Media Player**. The architecture decisions are based from the need to keep manual intervention to a minimum by striving for an automatic pipeline from software changes to build to deployment of the Dapp to the cloud. Then managing this infrastructure automatically and by code. Ultimately should lead to better performance, cost savings and automatic scaling to meet whatever workload that is thrown at it.

  

## Overview

  

YouTube supports around 30 formats for each video file uploaded, to allow good video streaming on multiple devices and resolutions. [For full list](#video-file-formats-supported-by-youtube)

| ID  | EXT   | RESOLUTION | FPS | CH | FILESIZE   | TBR   | PROTO | VCODEC      | VBR   | ACODEC     | ABR  | ASR | MORE INFO           |
| --- | ----- | ---------- | --- | -- | ---------- | ----- | ----- | ----------- | ----- | ---------- | ---- | --- | ------------------- |
| 136 | mp4   | 1280x720   | 12  |    |  179.39MiB |  632k | https | avc1.4d401f |  632k | video only |      |     | 720p, mp4_dash      |
| 247 | webm  | 1280x720   | 12  |    |  165.61MiB |  584k | https | vp9         |  584k | video only |      |     | 720p, webm_dash     |
| 137 | mp4   | 1920x1080  | 12  |    |  547.81MiB | 1931k | https | avc1.640028 | 1931k | video only |      |     | 1080p, mp4_dash     |
| 248 | webm  | 1920x1080  | 12  |    |  307.81MiB | 1085k | https | vp9         | 1085k | video only |      |     | 1080p, webm_dash    |
| 271 | webm  | 2560x1440  | 12  |    |  766.29MiB | 2701k | https | vp9         | 2701k | video only |      |     | 1440p, webm_dash    |
| 313 | webm  | 3840x2160  | 12  |    |    2.69GiB | 9695k | https | vp9         | 9695k | video only |      |     | 2160p, webm_dash    |

Fabstir Media Player will support similar, including the latest open source format [AV1](#glossary)

When a video file is uploaded to the Fabstir media player:

* JavaScript/TypeScript browser code uses Next.js to upload the video file to the server

* A service (C++ binary) listens to the server's upload directory for changes and transcodes uploaded video files to multiple formats/resolutions.

* Node.js listens to the server's output directory to upload transcoded files from there to [S5](#glossary) for storage to decentralised storage providers. A similar pipeline for LumeWeb can be in place when it is ready.
 

Audio files are treated the same way with outputs to different bitrates and compression from lossy to lossless.
  

## Table of Contents

- [Fabstir Web3 Media Player - Progress Report (Jan 2023)](#fabstir-web3-media-player---progress-report-jan-2023)
  - [Overview](#overview)
  - [Table of Contents](#table-of-contents)
  - [Infrastructure](#infrastructure)
    - [Kubernetes](#kubernetes)
    - [Argo CD](#argo-cd)
    - [Kustomize](#kustomize)
    - [GitHub Actions](#github-actions)
  - [Skills](#skills)
    - [DevOps](#devops)
    - [C++ 17/20](#c-1720)
  - [Conclusion](#conclusion)
  - [Appendix](#appendix)
    - [Video file formats supported by YouTube](#video-file-formats-supported-by-youtube)
  - [Glossary](#glossary)
  

## Infrastructure

Fabstir Media Player is architectured to handle mainstream workload usage from the start. In order to achieve this, the philosophy of infrastructure as code (IaC) is used. Fabstir uses [Kubernetes](#glossary) and other open source tools to provide its services as an automatically cloud managed cluster of server nodes. What this means is that Fabstir will

* Be able to spin new nodes in the cloud to scale to usage demand.

* Conversely, will prune nodes when demand drops to minimise resource use and costs.

* Allow for continuous updates without any downtime as updated nodes are swapped one at a time for old ones.

* Automatic rollback if need be to previous versions or state.

* Load balancing across nodes.

* Support multiple cloud providers from more cost effective providers up to GCP, AWS etc.

  

### Kubernetes

<p  align="center">

<img  align="center"  alt="Argo CD for Kubernetes"  src="https://fabstir.com/img2/Kubernetes_p1.jpg">

</p>

  

Kubernetes is an open-source container orchestration system for automating the deployment, scaling, and management of containerised pods. A single pod will represent a docker container that houses the running processes to deliver the front-end pages of the Dapp and the media transcoding service for video/audio files. Any pod will be able to upload or download media files to decentralised storage via S5.

  

Fabstir's infrastructure will be deployed across multiple cloud providers using a single Kubernetes cluster source. This makes the Dapp resilient to censorship and the whole cluster infrastructure can be easily deployed to other cloud providers if they support Kubernetes from its YAML configuration scripts. Tools [Argo CD](#glossary) and [Kustomize](#glossary) will be used to facilitate this.

  

### Argo CD

  

Argo CD is deployed into Kubernetes to allow it to monitor and sync the cluster of nodes to what is declaratively specified in YAML configuration (manifest) files stored in a **GitOps** repository. The repository can be considered the source of truth for the desired state of Fabstir's cluster configuration. For example if there is a manual change to the required number of nodes to run the Dapp by editing the configuration file in this repository, it will be detected by Argo CD that then makes the necessary changes to the cluster deployment to keep it in sync with the manifest files.

  

<p  align="center">

<img  align="center"  alt="Argo CD'S web-based GUI"  src="https://fabstir.com/img2/ArgoCD_p2.jpg">

</p>

  

Argo CD has a useful GUI interface to view the status of the deployment.

>  **Note:** After a successful commit/merge of the Dapp's source code, GitHub Actions can be used to automatically trigger Argo CD to deploy the changes. Explained later in the [GitHub-Actions](#github-actions) section.

  

### Kustomize

Fabstir uses Kustomize not only to easily allow for different instances of deployment stages of the cluster (development, staging and production) but also for multiple instances of the infrastructure across various cloud providers.

  

<p  align="center">

<img  align="center"  alt="Kustomize"  src="https://fabstir.com/img2/Kustomize_p1.jpg">

</p>

  

The GitOps repo will have all the configuration files that enables reconstruction of the infrastructure on to different cloud providers, with Kustomize used to supply overlays (YAML files) that describe only the custom changes needed to configure for each provider. Typical details would include different URL destination address and different resource set ups etc. For more [details](https://cloud.google.com/anthos-config-management/docs/concepts/kustomize).

  

### GitHub Actions

  

So far this report has talked about the **continuous deployment (CD)** side where a change in the Kubernetes, Kustomize or Argo CD YAML files in the GitOps repo automatically triggers Argo CD to change Fabstir's deployed clusters to match the configurations in the repo.

  

<p  align="center">

<img  align="center"  width=600  alt="GitHub Actions"  src="https://fabstir.com/img2/GitHubActions_p1.jpg">

</p>

  

**Continuous integration (CI)** however, is a software development practice in which code changes to the application leads to commits or pull requests that trigger automated builds and test runs to ensure that the changes do not break the existing codebase. In GitHub, continuous integration is implemented using its tool [GitHub Actions](#glossary).

There are two repos for Fabstir Web3 Media Player; one for its application source code and the other a **GitOps repo**. A GitOps repo is the configuration files for an application or infrastructure, as well as the automation scripts and tools needed to deploy and manage that application or infrastructure.

After a successful commit or merge, GitHub Actions writes an update to the GitOps repo for the new docker image build that triggers Argo CD to sync Fabstir's deployed clusters to match the configuration files in the repo. Hence the workflow from committing/merging code changes to deployment will be automatic and seamless.

  

>  **Note:** Having a separate (GitOps) repo for the Dapp configuration files means that infrastructure changes are version controlled and rollbacks can be done by simply going back to a previous version in GitHub. Plus uses Git to assign access control to only those authorised to make changes directly to the configuration files.

  

## Skills

  

### DevOps

Learnt [DevOps](#glossary) skills that include Docker, Kubernetes, GitHub Actions, Kustomize and Argo CD.

  

### C++ 17/20

C++ is still the go to language for media encoding and transcoding, largely due to the fact that FFmpeg is written in C/C++ and has to be compiled from source. Learning C++17/20 is like learning a new language except with all the baggage of the older C++ paradigms. The transcoder code will run as a service in a Docker image, listening to files uploaded to it and then carrying out transcoding to output to multiple media files.

  

## Conclusion

  

Fabstir Web3 Media Player's architecture will follow CI/CD (Continuous Integration and Continuous Deployment) best software development practices to enable automatic building, testing, and deploying of application code changes to production. The goal is to catch and fix errors as early as possible in the development process and to ensure that new code changes can be quickly and safely deployed to users. This can be achieved by using a set of tools that include GitHub Actions, Docker, Kubernetes, Argo CD and Kustomize that automate the build, test and deployment process. As shown by this BPMN diagram:

  

<p  align="center">

<img  align="center"  alt="Fabstir deployment workflow"  src="https://fabstir.com/img2/Fabstir_deployment_workflow.png">

</p>

  

Argo CD has a GUI to view the actual status of the cluster. Deployment configuration changes are all version controlled in a separate GitHub (GitOps) repo to allow rollback of the deployed infrastructure by simply rolling back to a previous version in GitHub.

Kustomize enables multiple instances of the cluster with minimal configuration files to enable development, staging and production instances. It also makes it easier to have multiple instances across different cloud providers, to enable Fabstir deployment to be more decentralised and scale to meet whatever the demands.

As just mentioned, with this architecture, Fabstir will be able to automatically scale to meet any traffic demand. It will embrace all the benefits of infrastructure by code (IaC) that include:

  

* Version control: IaC allows for infrastructure to be managed in a version control system, which allows for better collaboration and tracking of changes.

* Reproducibility: IaC allows for the creation of repeatable and consistent infrastructure, which can be easily reproduced in different environments.

* Automation: IaC allows for the automation of tasks such as provisioning, scaling, and deploying infrastructure, which can save time and reduce errors.

* Scalability: IaC allows for the scaling of infrastructure resources in a more efficient and automated manner.

* Cost Savings: IaC allows for efficient use of resources and reduces the need for manual labor, this leads to cost savings.

* Improved security: IaC enables for clear visibility of infrastructure and make changes to increase security.

* Disaster recovery: IaC allows to easily recover from a disaster by quickly rebuilding the infrastructure.
    

## Appendix
 

### Video file formats supported by YouTube

| ID  | EXT   | RESOLUTION | FPS | CH | FILESIZE   | TBR   | PROTO | VCODEC      | VBR   | ACODEC     | ABR  | ASR | MORE INFO           |
| --- | ----- | ---------- | --- | -- | ---------- | ----- | ----- | ----------- | ----- | ---------- | ---- | --- | ------------------- |
| sb2 | mhtml | 48x27      | 0   |    |            |       | mhtml | images      |       |            |      |     | storyboard          |
| sb1 | mhtml | 80x45      | 0   |    |            |       | mhtml | images      |       |            |      |     | storyboard          |
| sb0 | mhtml | 160x90     | 0   |    |            |       | mhtml | images      |       |            |      |     | storyboard          |
| 599 | m4a   | audio only |     | 2  |    8.73MiB |   31k | https | audio only  |       | mp4a.40.5  |  31k | 22k | ultralow, m4a_dash  |
| 600 | webm  | audio only |     | 2  |   10.08MiB |   36k | https | audio only  |       | opus       |  36k | 48k | ultralow, webm_dash |
| 139 | m4a   | audio only |     | 2  |   13.84MiB |   49k | https | audio only  |       | mp4a.40.5  |  49k | 22k | low, m4a_dash       |
| 249 | webm  | audio only |     | 2  |   14.77MiB |   52k | https | audio only  |       | opus       |  52k | 48k | low, webm_dash      |
| 250 | webm  | audio only |     | 2  |   19.43MiB |   68k | https | audio only  |       | opus       |  68k | 48k | low, webm_dash      |
| 140 | m4a   | audio only |     | 2  |   36.73MiB |  129k | https | audio only  |       | mp4a.40.2  | 129k | 44k | medium, m4a_dash    |
| 251 | webm  | audio only |     | 2  |   38.38MiB |  135k | https | audio only  |       | opus       | 135k | 48k | medium, webm_dash   |
| 17  | 3gp   | 176x144    | 12  | 1  |   20.89MiB |   74k | https | mp4v.20.3   |   74k | mp4a.40.2  |   0k | 22k | 144p                |
| 597 | mp4   | 256x144    | 12  |    |    8.94MiB |   32k | https | avc1.4d400b |   32k | video only |      |     | 144p, mp4_dash      |
| 160 | mp4   | 256x144    | 12  |    |   11.60MiB |   41k | https | avc1.4d400b |   41k | video only |      |     | 144p, mp4_dash      |
| 598 | webm  | 256x144    | 12  |    |    7.00MiB |   25k | https | vp9         |   25k | video only |      |     | 144p, webm_dash     |
| 278 | webm  | 256x144    | 12  |    |   17.30MiB |   61k | https | vp9         |   61k | video only |      |     | 144p, webm_dash     |
| 133 | mp4   | 426x240    | 12  |    |   26.73MiB |   94k | https | avc1.4d4015 |   94k | video only |      |     | 240p, mp4_dash      |
| 242 | webm  | 426x240    | 12  |    |   25.66MiB |   90k | https | vp9         |   90k | video only |      |     | 240p, webm_dash     |
| 134 | mp4   | 640x360    | 12  |    |   61.22MiB |  216k | https | avc1.4d4016 |  216k | video only |      |     | 360p, mp4_dash      |
| 18  | mp4   | 640x360    | 12  | 2  |  139.38MiB |  491k | https | avc1.42001E |  491k | mp4a.40.2  |   0k | 44k | 360p                |
| 243 | webm  | 640x360    | 12  |    |   57.74MiB |  204k | https | vp9         |  204k | video only |      |     | 360p, webm_dash     |
| 135 | mp4   | 854x480    | 12  |    |  127.84MiB |  451k | https | avc1.4d4016 |  451k | video only |      |     | 480p, mp4_dash      |
| 244 | webm  | 854x480    | 12  |    |   86.16MiB |  304k | https | vp9         |  304k | video only |      |     | 480p, webm_dash     |
| 22  | mp4   | 1280x720   | 12  | 2  | ~221.24MiB |  762k | https | avc1.64001F |  762k | mp4a.40.2  |   0k | 44k | 720p                |
| 136 | mp4   | 1280x720   | 12  |    |  179.39MiB |  632k | https | avc1.4d401f |  632k | video only |      |     | 720p, mp4_dash      |
| 247 | webm  | 1280x720   | 12  |    |  165.61MiB |  584k | https | vp9         |  584k | video only |      |     | 720p, webm_dash     |
| 137 | mp4   | 1920x1080  | 12  |    |  547.81MiB | 1931k | https | avc1.640028 | 1931k | video only |      |     | 1080p, mp4_dash     |
| 248 | webm  | 1920x1080  | 12  |    |  307.81MiB | 1085k | https | vp9         | 1085k | video only |      |     | 1080p, webm_dash    |
| 271 | webm  | 2560x1440  | 12  |    |  766.29MiB | 2701k | https | vp9         | 2701k | video only |      |     | 1440p, webm_dash    |
| 313 | webm  | 3840x2160  | 12  |    |    2.69GiB | 9695k | https | vp9         | 9695k | video only |      |     | 2160p, webm_dash    |


## Glossary

  
  

Argo CD

  

: Argo CD is a declarative, GitOps continuous delivery tool for Kubernetes. It allows to manage and deploy applications declaratively, by using a Git repository as the source of truth for the desired state of the applications running on a cluster.

  

AV1

  

: AV1 is an open-source, royalty-free video compression format developed by the Alliance for Open Media (AOMedia). It is designed to improve upon the VP9 and H.265/HEVC formats

  

DevOps

  

: DevOps is a set of practices and tools that aim to improve the collaboration, automation and communication between the development and operations teams. The goal of DevOps is to allow organizations to deliver software faster and more frequently, with higher quality and fewer errors. DevOps practices include continuous integration, continuous delivery, containerization, and infrastructure as code, among others. These practices are designed to help organizations to be more agile, efficient and to reduce the time to market for new features and products.

  

GitHub Actions

  

: Continuous integration (CI) in GitHub is the practice of regularly integrating code changes into a shared repository and running automated tests to ensure that the codebase remains stable. This can be achieved through the use of tools such as GitHub Actions, that allow developers to set up custom workflows that are triggered by specific events, such as the creation of a pull request or the pushing of code to a repository. This enables developers to automatically test and deploy their code, and to quickly identify and fix any issues that may arise.

  

Kubernetes

  

: Kubernetes is an open-source container orchestration system that automates the deployment, scaling, and management of containerized applications. It provides a way to manage and scale containers across multiple hosts, making it easy to run and manage containerized applications in a variety of environments. Kubernetes provides features like automatic scaling, rolling updates, self-healing, and automatic load balancing. It also offers a centralized control plane for monitoring and managing the state of all the containers in a cluster and supports multiple container runtimes and platforms. It is widely used in industry and in the cloud-native ecosystem.

  

Kustomize

  

: Kustomize is a tool for customizing Kubernetes YAML files, which allows users to easily customize and manage complex Kubernetes manifests. It provides a simple and flexible way to customize resources without having to create new YAML files from scratch or modify existing ones. Kustomize uses a set of patching and variable substitution rules to modify existing manifests, and supports different levels of customization, from simple variable substitution to more complex patching and overlay strategies. It can be used as a command-line tool, as well as integrated with other tools such as kubectl and Helm.

  

S5

  

: S5 is a decentralized network that puts you in control of your data and identity. At its core, it is a content-addressed storage network similar to IPFS, but with some new concepts and ideas to make it more efficient and powerful. All relevant code can be found here: [https://github.com/s5-dev](https://github.com/s5-dev)
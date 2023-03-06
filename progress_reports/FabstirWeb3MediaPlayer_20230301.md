# Fabstir Web3 Media Player - Progress Report (Feb 2023)

This February report update is organized according to the order in which the work was done. For words that may not be common knowledge (unless one comes from a development background), a subscript digit is placed next to the word in question. When clicked, it will take the reader to the word's brief explanation in the glossary. Moreover, a return arrow symbol is also provided, which allows the reader to return to where they left off.

## Learning Rust

At first, I was eager to start coding and delve deep into the project. However, considering the long-term nature of this FOSS project, it would be a tough challenge for those who don't know C++ to learn the language and write safe code proficiently.

Therefore, I decided to learn Rust instead, which caused a two-week delay before I could resume where I left off. Although Rust's memory model and compiler may take some time to get used to, in my opinion, its code safety feature, especially in concurrent programming, is worth it. Once the program compiles, one can be much more confident that it works as intended. Furthermore, Rust's performance is just as good as that of C++.

Before I explain what I coded in Rust, I'll rewind a little bit.

## Cloud Infrastructure Explanation

![Fabstir cloud infrastructure](https://fabstir.com/files/reports/FabstirMediaPlayer_Infrastructure_d1b.jpg)

"This diagram may seem complicated, but it represents Fabstir Media Player's network cloud computing Kubernetes[^Kubernetes] infrastructure designed to handle thousands of users. It is divided into two main clusters:

-   The Akash Network cluster consists of decentralized computer nodes that run the Fabstir Media Player Dapp.
-   The other cluster is responsible for transcoding videos and music into various formats to enable smooth playback, regardless of the end-users' device's bitrate or screen resolution. When in live production, this will be a group of clusters one per GPU cloud provider, where market prices and some randomness will dictate which of the providers will receive the GPU workload per transcode job to be done.

Both clusters store their data in SIA storage via [S5](https://github.com/s5-dev/S5), from which video and audio are streamed. Whenever changes are made to the media player or transcoder code and pushed to their respective GitHub repositories, it initiates a chain reaction:

[1]: GitHub Actions[^GitHubActions] listens for changes in the source code repositories for the media player or transcoder and runs their respective unit tests. If the tests pass, their GitHub manifest repositories are updated.
[2]: ArgoCD[^ArgoCD] listens for changes in the manifest[^Manifest] repository. Once a change is detected, it triggers Kubernetes to run the updated manifest files to deploy the necessary updates to the Kubernetes clusters.
[3]: End-users experience no downtime when software updates are rolled out, as the existing pods[^Pod] are gradually replaced with new ones that match the updated configuration of the manifest repositories.

> **Note** I haven't tested Horizontal Pod Autoscaler (HPA)[^HPA] yet, which can automatically adjust the number of replicas in a Kubernetes deployment based on CPU/GPU utilization, memory usage, or other metrics.

## Testing the Infrastructure
I conducted my initial tests on MiniKube[^MiniKube], using ExpressJS[^ExpressJS] for the server-side code. I used JavaScript to serve a webpage that allows users to browse for a video file and upload it to a Kubernetes pod[^Pod] by clicking 'Submit'. Upon receiving the file, the pod simultaneously uploads it to S5 for storage on SIA and calls a transcode method on the Transcoder cluster via gRPC[^gRPC].
The end-users do not realise that the dapp is split across different clusters and pods, the just see and interact with the web pages that are served to them.

## The Transcode Process
The transcoder is written in Rust, and it calls [ffmpeg](https://github.com/FFmpeg/FFmpeg), a C++ library, to perform the transcoding work. When the Rust server's `transcode` method is called with the file path to transcode, the job is added to a queue. Another thread picks up the job from the queue to call ffmpeg, and the transcoded file is then stored in a temporary directory on the pod.

From there, the file will be uploaded to S5's endpoint using the TUS[^TUS] protocol, where it gets stored in SIA storage. For the successful test, an h264 file in .mp4 format was uploaded and transcoded to two resolutions: 1080p and 720p.

## Conclusion
- Switched to Rust from C++ for the transcoder server code.
- Set up local MiniKubes on my PC to test the media player/transcoder infrastructures.
- Uploaded a video to the media player cluster successfully, which was then uploaded to S5 for storage on SIA.
- The server code then successfully called the transcoder infrastructure to transcode the file to h264 1080p and 720p .mp4 formats.
- Added authorisation token functionality to the `tus_client` Rust native code, enabling Redsolver's code snippet to upload files with authorisation.
- Successfully tested the upload of transcoded videos to S5 for storage on SIA.
- Checked that transcoded videos can be streamed successfully from SIA using S5's player.
- Integrated Redsolver's S5 code into my test browser/server-side code and able to successfully play the transcoded footage in the browser.

I have started reaching out to cloud computing providers, and the reception has been positive. Notably, one provider has expressed interest in the integration of Web3 technology into their services, and to collaborate closely with Fabstir. More news to come.

## Glossary
[^ArgoCD]: **ArgoCD:** ArgoCD is an open-source continuous delivery tool that helps automate the deployment of applications to Kubernetes clusters. It uses GitOps principles to synchronize the desired state of the deployed applications with the actual state in the cluster. With ArgoCD, users can define the desired state of their application in a Git repository, and ArgoCD will automatically deploy and manage the application to the target Kubernetes cluster. It provides a web-based user interface and a command-line interface for managing and monitoring the deployed applications.

[^ExpressJS]: **ExpressJS** ExpressJS is a fast and minimalist web framework for Node.js that provides a set of robust features for building web applications and APIs. It is lightweight, flexible, and designed to handle middleware to perform various HTTP requests and responses. ExpressJS is highly customizable and allows developers to build applications quickly and efficiently using simple and intuitive syntax. It is widely used by developers to build scalable, reliable, and performant web applications. ExpressJS has a vast ecosystem of plugins and modules that make it easy to integrate with other technologies and frameworks.

[^GitHubActions]: **GitHub Actions:** GitHub Actions is a powerful workflow automation tool provided by GitHub that allows developers to automate their software development workflows. It enables users to define custom actions that can be triggered by events, such as code commits, pull requests, or issues. With GitHub Actions, developers can automate tasks such as building, testing, and deploying code, as well as create custom workflows tailored to their specific needs.

[^gRPC]: **gRPC** gRPC is a high-performance, open-source remote procedure call (RPC) framework developed by Google. It uses the Protocol Buffers data serialization format and communicates over HTTP/2, allowing clients to call methods on remote servers using simple APIs. gRPC offers high performance, automatic code generation, bidirectional streaming, flow control, authentication, and load balancing, making it ideal for building distributed systems that require high performance and scalability.

[^HPA]: **Horizontal Pod Autoscaler** Horizontal Pod Autoscaler (HPA) is a Kubernetes feature that automatically adjusts the number of replicas in a deployment or replica set based on observed CPU utilization or custom metrics of the running pods, allowing the cluster to scale the number of pods in response to changes in traffic or application demand.

[^Kubernetes]: **Kubernetes:** Kubernetes is an open-source container orchestration platform that helps manage and deploy containerized applications at scale. It automates the deployment, scaling, and management of containerized applications across a cluster of nodes. A Kubernetes cluster consists of a master node that manages the overall state of the cluster and worker nodes that run the containers. By abstracting away the underlying infrastructure, Kubernetes makes it easier to deploy and manage complex applications across a cluster of machines.

[^Manifest]: **Manifest:** A manifest YAML file is a file written in YAML (Yet Another Markup Language) format that defines the desired state of a Kubernetes resource or set of resources. It typically contains information such as the name, type, and configuration parameters of the Kubernetes resource, as well as any dependencies or relationships with other resources. Manifest YAML files are used to deploy and manage applications and services on Kubernetes clusters, and can be version-controlled and managed like any other code file.

[^MiniKube]: **MiniKube:** MiniKube is a tool that allows users to run a single-node Kubernetes cluster on their local machine for testing and development purposes. It provides a lightweight and easy-to-use platform for developers to experiment with Kubernetes features and deploy applications in a local environment. MiniKube runs as a virtual machine on the local machine, and provides a command-line interface for managing the Kubernetes cluster and deploying applications. It supports multiple virtualization platforms, such as VirtualBox and KVM, and can be used with a variety of operating systems, including Windows, macOS, and Linux.

[^Pod]: **Pod** A Kubernetes pod is the smallest deployable unit in Kubernetes that represents a single instance of a running process in a cluster. It can contain one or more containers that share the same network namespace and storage resources.

[^S5]: **S5 :** S5 is a new decentralised content-addressed storage network that uses unique hash value generated from the content to store and retrieve its data. It supports a number of storage providers, SIA being one of them.

[^Transcoder]: **Transcoder:**  A video transcoder is a software or hardware tool that converts video files from one format to another, while preserving the quality of the original video as much as possible. Video transcoding is often used to make video files compatible with different devices or platforms, or to reduce the size of the video file for more efficient storage or streaming. Video transcoders can also be used to convert video files into different resolutions, bitrates, or codecs to optimize the playback experience on different devices or network conditions.

[^TUS]: **TUS** The TUS protocol is an open-source protocol for resumable file uploads that allows clients to pause and resume file uploads, even after network interruptions. It uses a set of HTTP endpoints and headers to handle file uploads and is designed to work with any backend storage system.

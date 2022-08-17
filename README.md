# code-with-quarkus-microshift Project

This project uses Quarkus, the Supersonic Subatomic Java Framework.

If you want to learn more about Quarkus, please visit its website: https://quarkus.io/ .

## Notes pushing to quay.io the multi arch

using JIB may take several time longer, at least the first time:

```
[INFO] --- quarkus-maven-plugin:2.11.2.Final:build (default) @ code-with-quarkus-microshift ---
[INFO] Checking for existing resources in: /Users/mmortari/git/code-with-quarkus-microshift/src/main/kubernetes.
[INFO] [io.quarkus.container.image.jib.deployment.JibProcessor] Starting (local) container image build for jar using jib.
[WARNING] [io.quarkus.container.image.jib.deployment.JibProcessor] Base image 'registry.access.redhat.com/ubi8/openjdk-17-runtime:1.11' does not use a specific image digest - build may not be reproducible
[INFO] [io.quarkus.container.image.jib.deployment.JibProcessor] Using base image with digest: sha256:1a2fddacdcda67494168749c7ab49243d06d8fbed34abab90566d81b94f5e1a5
[INFO] [io.quarkus.container.image.jib.deployment.JibProcessor] Container entrypoint set to [java, -Djava.util.logging.manager=org.jboss.logmanager.LogManager, -jar, quarkus-run.jar]
[INFO] [io.quarkus.container.image.jib.deployment.JibProcessor] Container entrypoint set to [java, -Djava.util.logging.manager=org.jboss.logmanager.LogManager, -jar, quarkus-run.jar]
[INFO] [io.quarkus.container.image.jib.deployment.JibProcessor] Pushed container image quay.io/mmortari/code-with-quarkus-microshift:1.0.0-SNAPSHOT (sha256:54e3a6814ea828230f35ad5892d1d040d2a455a7815a168f0914a42e14086264)

[INFO] [io.quarkus.deployment.QuarkusAugmentor] Quarkus augmentation completed in 349360ms
```

if compared to using docker buildx

```
[INFO] --- quarkus-maven-plugin:2.11.2.Final:build (default) @ code-with-quarkus-microshift ---
[INFO] Checking for existing resources in: /Users/mmortari/git/code-with-quarkus-microshift/src/main/kubernetes.
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] Starting (local) container image build for jar using docker.
[INFO] [io.quarkus.deployment.util.ExecUtil] WARNING! Using --password via the CLI is insecure. Use --password-stdin.
[INFO] [io.quarkus.deployment.util.ExecUtil] Login Succeeded
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] Executing the following command to build docker image: 'docker buildx build -f /Users/mmortari/git/code-with-quarkus-microshift/src/main/docker/Dockerfile.jvm --platform linux/amd64,linux/arm64 -t quay.io/mmortari/code-with-quarkus-microshift:1.0.0-SNAPSHOT --push /Users/mmortari/git/code-with-quarkus-microshift'
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #1 [internal] load build definition from Dockerfile.jvm
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #1 transferring dockerfile: 5.41kB done
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #1 DONE 0.0s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #2 [internal] load .dockerignore
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #2 transferring context: 198B done
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #2 DONE 0.0s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #3 [linux/arm64 internal] load metadata for registry.access.redhat.com/ubi8/openjdk-17:1.11
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #3 DONE 0.3s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #4 [linux/amd64 internal] load metadata for registry.access.redhat.com/ubi8/openjdk-17:1.11
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #4 DONE 0.6s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #5 [linux/amd64 1/5] FROM registry.access.redhat.com/ubi8/openjdk-17:1.11@sha256:e2c7f23132ef04d94b735d58f7dd544088cf46cb23415e902ae446c45fc9268a
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #5 resolve registry.access.redhat.com/ubi8/openjdk-17:1.11@sha256:e2c7f23132ef04d94b735d58f7dd544088cf46cb23415e902ae446c45fc9268a 0.0s done
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #5 DONE 0.0s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #6 [linux/arm64 1/5] FROM registry.access.redhat.com/ubi8/openjdk-17:1.11@sha256:e2c7f23132ef04d94b735d58f7dd544088cf46cb23415e902ae446c45fc9268a
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #6 resolve registry.access.redhat.com/ubi8/openjdk-17:1.11@sha256:e2c7f23132ef04d94b735d58f7dd544088cf46cb23415e902ae446c45fc9268a 0.0s done
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #6 DONE 0.0s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #7 [internal] load build context
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #7 transferring context: 17.84MB 0.3s done
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #7 DONE 0.3s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #6 [linux/arm64 1/5] FROM registry.access.redhat.com/ubi8/openjdk-17:1.11@sha256:e2c7f23132ef04d94b735d58f7dd544088cf46cb23415e902ae446c45fc9268a
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #6 CACHED
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #5 [linux/amd64 1/5] FROM registry.access.redhat.com/ubi8/openjdk-17:1.11@sha256:e2c7f23132ef04d94b735d58f7dd544088cf46cb23415e902ae446c45fc9268a
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #5 CACHED
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #8 [linux/amd64 2/5] COPY --chown=185 target/quarkus-app/lib/ /deployments/lib/
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #8 DONE 0.1s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #9 [linux/arm64 2/5] COPY --chown=185 target/quarkus-app/lib/ /deployments/lib/
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #9 DONE 0.1s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #10 [linux/amd64 3/5] COPY --chown=185 target/quarkus-app/*.jar /deployments/
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #10 DONE 0.0s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #11 [linux/arm64 3/5] COPY --chown=185 target/quarkus-app/*.jar /deployments/
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #11 DONE 0.0s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #12 [linux/arm64 4/5] COPY --chown=185 target/quarkus-app/app/ /deployments/app/
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #12 DONE 0.1s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #13 [linux/amd64 4/5] COPY --chown=185 target/quarkus-app/app/ /deployments/app/
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #13 DONE 0.1s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #14 [linux/arm64 5/5] COPY --chown=185 target/quarkus-app/quarkus/ /deployments/quarkus/
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #14 DONE 0.0s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #15 [linux/amd64 5/5] COPY --chown=185 target/quarkus-app/quarkus/ /deployments/quarkus/
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #15 DONE 0.0s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 exporting to image
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 exporting layers
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 exporting layers 0.5s done
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 exporting manifest sha256:eafc6760b8db11bcf633821b4fa136374e187220e1c88e755c07bf41f57e9760 done
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 exporting config sha256:72799abfc28112f83397b4031ccfc532c99d4acc60e9f637eaff05102dfa99d6 done
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 exporting manifest sha256:3f209ff4eeed112d6ee13dd7699f07a3efacf752e1a1ad73d623c2b01cb049f1 done
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 exporting config sha256:3ca763488d6b54a13e4cde679f8dd98a812abf3dc6428f23ffc45fc3819c99d6 done
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 exporting manifest list sha256:754cf8f850e63d145493f2eb519f8b94095194c1d370923a01f637761d3f0df0 done
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 pushing layers
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 ...
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #17 [auth] mmortari/code-with-quarkus-microshift:pull,push token for quay.io
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #17 DONE 0.0s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] 
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 exporting to image
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 pushing layers 167.9s done
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 pushing manifest for quay.io/mmortari/code-with-quarkus-microshift:1.0.0-SNAPSHOT@sha256:754cf8f850e63d145493f2eb519f8b94095194c1d370923a01f637761d3f0df0
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 pushing manifest for quay.io/mmortari/code-with-quarkus-microshift:1.0.0-SNAPSHOT@sha256:754cf8f850e63d145493f2eb519f8b94095194c1d370923a01f637761d3f0df0 2.8s done
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] #16 DONE 171.4s
[INFO] [io.quarkus.container.image.docker.deployment.DockerProcessor] Built container image quay.io/mmortari/code-with-quarkus-microshift:1.0.0-SNAPSHOT (linux/amd64,linux/arm64 platform(s))

[INFO] [io.quarkus.deployment.QuarkusAugmentor] Quarkus augmentation completed in 176753ms
```

but subsequent tag push with jib looks faster:

```
[INFO] --- quarkus-maven-plugin:2.11.2.Final:build (default) @ code-with-quarkus-microshift ---
[INFO] Checking for existing resources in: /Users/mmortari/git/code-with-quarkus-microshift/src/main/kubernetes.
[INFO] [io.quarkus.container.image.jib.deployment.JibProcessor] Starting (local) container image build for jar using jib.
[WARNING] [io.quarkus.container.image.jib.deployment.JibProcessor] Base image 'registry.access.redhat.com/ubi8/openjdk-17-runtime:1.11' does not use a specific image digest - build may not be reproducible
[INFO] [io.quarkus.container.image.jib.deployment.JibProcessor] Using base image with digest: sha256:1a2fddacdcda67494168749c7ab49243d06d8fbed34abab90566d81b94f5e1a5
[INFO] [io.quarkus.container.image.jib.deployment.JibProcessor] Container entrypoint set to [java, -Djava.util.logging.manager=org.jboss.logmanager.LogManager, -jar, quarkus-run.jar]
[INFO] [io.quarkus.container.image.jib.deployment.JibProcessor] Container entrypoint set to [java, -Djava.util.logging.manager=org.jboss.logmanager.LogManager, -jar, quarkus-run.jar]
[INFO] [io.quarkus.container.image.jib.deployment.JibProcessor] Pushed container image quay.io/mmortari/code-with-quarkus-microshift:1.0.0-SNAPSHOT (sha256:c3fcd0b96e4ace5bc9a40f3fa21c9c4b41f3db8e2b6afefbbde04df632253929)

[INFO] [io.quarkus.deployment.QuarkusAugmentor] Quarkus augmentation completed in 64666ms
```

<!--
## Running the application in dev mode

You can run your application in dev mode that enables live coding using:
```shell script
./mvnw compile quarkus:dev
```

> **_NOTE:_**  Quarkus now ships with a Dev UI, which is available in dev mode only at http://localhost:8080/q/dev/.

## Packaging and running the application

The application can be packaged using:
```shell script
./mvnw package
```
It produces the `quarkus-run.jar` file in the `target/quarkus-app/` directory.
Be aware that it’s not an _über-jar_ as the dependencies are copied into the `target/quarkus-app/lib/` directory.

The application is now runnable using `java -jar target/quarkus-app/quarkus-run.jar`.

If you want to build an _über-jar_, execute the following command:
```shell script
./mvnw package -Dquarkus.package.type=uber-jar
```

The application, packaged as an _über-jar_, is now runnable using `java -jar target/*-runner.jar`.

## Creating a native executable

You can create a native executable using: 
```shell script
./mvnw package -Pnative
```

Or, if you don't have GraalVM installed, you can run the native executable build in a container using: 
```shell script
./mvnw package -Pnative -Dquarkus.native.container-build=true
```

You can then execute your native executable with: `./target/code-with-quarkus-microshift-1.0.0-SNAPSHOT-runner`

If you want to learn more about building native executables, please consult https://quarkus.io/guides/maven-tooling.

## Related Guides

- SmallRye OpenAPI ([guide](https://quarkus.io/guides/openapi-swaggerui)): Document your REST APIs with OpenAPI - comes with Swagger UI
- RESTEasy Reactive ([guide](https://quarkus.io/guides/resteasy-reactive)): A JAX-RS implementation utilizing build time processing and Vert.x. This extension is not compatible with the quarkus-resteasy extension, or any of the extensions that depend on it.
- Kubernetes ([guide](https://quarkus.io/guides/kubernetes)): Generate Kubernetes resources from annotations

## Provided Code

### RESTEasy Reactive

Easily start your Reactive RESTful Web Services

[Related guide section...](https://quarkus.io/guides/getting-started-reactive#reactive-jax-rs-resources)
-->
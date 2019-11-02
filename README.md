# Docker and kubernetes

This project is a part of the course `Docker and k8s` ([lecture](https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/))

## Docker
- **Imperative Deployments** : Do exactly these steps to arrive at this container setup

## k8s
- **Declarative Deployments** : Out container setup should look like this, make it happe!
  - 물론, k8s은 imperative한 방법도 제공한다.
  - 블로그 글, k8s doc 볼때 **declarative**/**imperative**한 방법 둘 다 있음을 생각한다.
  - **하지만, 실제 production 환경에서는 무조건 declarative 한 방법만 사용해야 한다.!!!!**
  - k8s는 언제나 **desired state** 의 상태로 가고자 한다. [참고](https://kubernetes.io/docs/concepts/)
- [이미지 태그 변경없이 pod 이미지 바꾸는 방법.](https://github.com/kubernetes/kubernetes/issues/33664)

## Document list
- [How to write Dockerfile](./documents/dockerfile.md)
- [How to use docker](./documents/docker.md)
- [How to use docker-compose](./documents/docker-compose.md)
- [k8s](./documents/k8s.md)

# Ref list
- [Docker Hub](https://hub.docker.com)
- [44bits](https://www.44bits.io/ko/post/almost-perfect-development-environment-with-docker-and-docker-compose)

## source code
- [Diagrams](https://github.com/StephenGrider/DockerCasts/tree/master/diagrams)
- [Main repository (includes Skaffold section)](https://github.com/StephenGrider/DockerCasts)
- [Completed code for the AWS React single container project](https://github.com/StephenGrider/docker-react)
- [Completed code for the AWS Multi Docker Project](https://github.com/StephenGrider/multi-docker)
- [Completed code for the Multi K8s Project](https://github.com/StephenGrider/multi-k8s)

## lectures
- [Multi-container Github and Travis CI Setup](https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/learn/lecture/11437336#questions)
- [k8s entire deployment flow](https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/learn/lecture/11482942#questions)
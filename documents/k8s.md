# kubernetes
## Summary
- k8s에서는 이미지를 빌드하는 일이 없다.
- k8s에서는 오직 object(pod, service, controller ..)를 배포한다.
- docker-compose 로 컨테이너를 운영하는 경우, 하나의 컨테이너가 죽어도 다른 컨테이너는 살아 있는 상태로 동작한다. 하지만, k8s 에서는 같은 서비스 목적으로 배포되는 컨테이너는 매우 강하게 결합(tightly coupled)되어 있기 때문에, 하나만 죽어도 전체가 다 죽는다.(pod 단위로 죽거나 살린다.)
- k8s는 label-selector 시스템을 사용한다. config 파일에서 직접적으로 다른 pod을 지칭하는 name을 쓰지 않고, `selector`에 정의된 `component` key-value pair를 사용한다. [[참고]](https://kubernetes.io/ko/docs/concepts/overview/working-with-objects/labels/)
  - `pod`에서 `label`을 붙이면, `service` 에서 `selector`로 선택한다.

## Glossary
> Object : k8s에 의해서 생성되는 가장 기본 구성단위

> apiVersion : k8s 에서 제공하는 API를 뜻함. 각 api 마다 기능이 다르기 때문에, 사용하는 용도에 따라 다른 API를 선택해야 한다.
[참고](https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-apiversion-definition-guide.html)

## minukube(VM)
### Our test environment
![Test environment](./images/k8s/environment.png)
- Node means VM

- kubernetes test environment ==> VM !!
> Going forward, any minikube commands run in the lecture videos can be ignored. Also, instead of the IP address used in the video lectures when using minikube, we use localhost.

> For example, in the first project where we deploy our simple React app, using minikube we would visit:
> 192.168.99.101:31515

> Instead, when using Docker Desktop's Kubernetes, we would visit: localhost:31515

> Also, you can skim through the discussion about needing to use the local Docker node in the "Multiple Docker Installations" and "Why Mess with Docker in the Node" lectures (187-189), this only applies to minikube users.

### minikube command
- minukube start/stop/status
- minukube ip

## Difference between `docker-compose` and `k8s`
- docker-compose can build image
- k8s only use already build image

![Diff](./images/k8s/diff-docker-k8s.png)

- Final goal

![Goal](./images/k8s/final-goal.png)

## k8s
### k8s commands
- kubectl cluster-info
- kubectl apply -f client-pod.yaml
  - create pod
- kubectl apply -f client-node-port.yaml
  - configure service
- kubectl get pods
  - show pods
```
youk@cs-macbook ~/workspace/udemy/simeplek8s ±master⚡ » kubectl get pods
NAME     READY   STATUS    RESTARTS   AGE
client   1/1     Running   0          2m39s
```
- kubectl get services
  - show services
 ```
youk@cs-macbook ~/workspace/udemy/simeplek8s ±master⚡ » kubectl get services
NAME               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
client-node-port   NodePort    10.111.123.240   <none>        3050:31515/TCP   2m25s
kubernetes         ClusterIP   10.96.0.1        <none>        443/TCP          107m
```
---------
> Service object
```
apiVersion: v1
kind: Service  <-- Type of object
metadata:
  name: client-node-port
spec:
  type: NodePort
  ports:
  - port: 3050  # <-- 다른 pod이 multi-client pod에 접속 할 수 있는 port
    targetPort: 3000 # <-- container port
    nodePort: 31515 # <-- exposed outside(access from webbrowser)
  selector:
    component: web
```

> Pod object
```
apiVersion: v1
kind: Pod
metadata:
  name: client
  labels:
    component: web  # It can be "tier: front", whatever key-value pair possible.
spec:
  containers:
  - name: client
    image: csyouk/multi-client
    ports:
      - containerPort: 3000
```

## kubernetes
### Object, Controller 개념
#### https://coding-start.tistory.com/308
#### Pod
```
apiVersion: v1 
kind: Pod 
metadata: 
  name: springboot-web 
spec: 
  containers: 
  - name: springboot-web 
    image: 1223yys/springboot-web:0.1.6 
    ports: 
    - containerPort: 8080
```
#### ReplicaSet
```
apiVersion: apps/v1
kind: ReplicaSet
metadata: 
  name: sample-replicaset
  labels:
    app: springboot-web
spec:
  replicas: 3
  selector:
    matchLabels:
      app: springboot-web
  template:
    metadata:
      labels:
        app: spring-web
    spec: 
    containers: 
    - name: springboot-web 
      image: 1223yys/springboot-web:0.1.6 
      ports: 
      - containerPort: 8080
```
#### Deployment
##### Deployment는 ReplicaSet과 크게 다르지 않고 ReplicaSet의 revision을 관리할수 있다 정도
#### Service
```
kind: Service
metadata: 
  name: sample-service
spec:
  selector:
    app: springboot-web
  ports:
    - port: 80
      protocol: TCP
      targetPort: 8080
```
#### Ingress
```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: hello-ingress
spec:
  rules:
  - http:
      paths:
      - path: /users/*
        backend:
          serviceName: users-node-svc
          servicePort: 80
      - path: /products/*
        backend:
          serviceName: products-node-svc
          servicePort: 80
```

##### https://kubernetes.io/ko/docs/concepts/overview/what-is-kubernetes/
### 서비스 디스커버리와 로드 밸런싱
#### 쿠버네티스는 DNS 이름을 사용하거나 자체 IP 주소를 사용하여 컨테이너를 노출할 수 있다. 컨테이너에 대한 트래픽이 많으면, 쿠버네티스는 네트워크 트래픽을 로드밸런싱하고 배포하여 배포가 안정적으로 이루어질 수 있다.
### 스토리지 오케스트레이션
#### 쿠버네티스를 사용하면 로컬 저장소, 공용 클라우드 공급자 등과 같이 원하는 저장소 시스템을 자동으로 탑재 할 수 있다.
#### 스토리지 종류: emptyDir,  hostPath, gitRepo, PersistentVolumn(+Dynamic Provisioning), Storage class
##### https://bcho.tistory.com/1259
### 자동화된 롤아웃과 롤백
#### 쿠버네티스를 사용하여 배포된 컨테이너의 원하는 상태를 서술할 수 있으며 현재 상태를 원하는 상태로 설정한 속도에 따라 변경할 수 있다. 예를 들어 쿠버네티스를 자동화해서 배포용 새 컨테이너를 만들고, 기존 컨테이너를 제거하고, 모든 리소스를 새 컨테이너에 적용할 수 있다.
#### 롤링 업데이트, 배포, 롤백
#### https://bcho.tistory.com/1266?category=731548
### 자동화된 빈 패킹 (bin packing)
#### 컨테이너화된 작업을 실행하는데 사용할 수 있는 쿠버네티스 클러스터 노드를 제공한다. 각 컨테이너가 필요로 하는 CPU와 메모리(RAM)를 쿠버네티스에게 지시한다. 쿠버네티스는 컨테이너를 노드에 맞추어서 리소스를 가장 잘 사용할 수 있도록 해준다.
```
apiVersion: v1
kind: LimitRange
metadata:
  name: mem-limit-range
spec:
  limits:
  - default:
      memory: 512Mi
    defaultRequest:
      memory: 256Mi
    type: Container
```
### 자동화된 복구 (self healing)
#### 쿠버네티스는 실패한 컨테이너를 다시 시작하고, 컨테이너를 교체하며, '사용자 정의 상태 검사'에 응답하지 않는 컨테이너를 죽이고, 서비스 준비가 끝날 때까지 그러한 과정을 클라이언트에 보여주지 않는다.
#### Liveness probe, Readiness probe
#### https://bcho.tistory.com/1264
### 시크릿과 구성 관리
#### 쿠버네티스를 사용하면 암호, OAuth 토큰 및 SSH 키와 같은 중요한 정보를 저장하고 관리 할 수 있다. 컨테이너 이미지를 재구성하지 않고 스택 구성에 시크릿을 노출하지 않고도 시크릿 및 애플리케이션 구성을 배포 및 업데이트 할 수 있다.
#### ConfigMap - Literal, File
#### https://bcho.tistory.com/1267


---
layout: single
title: "Kubernetes - ReplicaSet"
categories: ['Cloud']
---

#### ReplicaSet
* 주어진 시간에 실행되는 안정적인 복제 Pod 세트를 유지
* 지정된 수의 동일한 Pod의 가용성을 보장하는 데 사용
* 운영 환경에서 Pod만 단독으로 사용하는 경우는 거의 없음

***

#### ReplicaSet API 확인
```
kubctl api-resources
```   
   

***

#### ReplicaSet Yaml 파일 작성
* kubweb-replicaset.yaml 파일 생성
* 파일 작성시 공백 2개로 들여쓰기 구분
* 수업 때는 vsCode를 이용해서 생성했다.
   
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: kuweb-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: kuweb-label
template:
  metadata:
    name: kuweb-pod
    labels:
      app: kuweb-label
  spec: 
    containers:
    - name: kuweb
      image: testweb:1.0
      ports:
      - containerPort: 8080
        protocol: TCP
```   

***

#### ReplicaSet 생성
```
kubectl apply -f <Yaml 파일 경로> [옵션]

kubectl apply -f d:\KubeTestWeb\kuweb-replicaset.yaml
```   
   
#### ReplicaSet 목록 확인
```
// 유지되는 Pod 개수 확인 가능
kubectl get replicasets [옵션]

// - replicaset의 Pod 선택기, 컨테이너이름, 이미지이름 확인 가능
// rs : replicasets의 짧은 명령어
kubectl get rs -o wide
```
   
***

#### ReplicaSet 상세 정보 확인
```
kubectl describe rs [옵션]

kubectl describe rs kuweb-replicaset
```   
   
***

#### ReplicaSet으로 생성된 Pod 정보 확인
* po : 명령어 pods
* Pod명은 Replicaset 이름+16진수 랜덤 값으로 자동 생성
   
```
kubectl get po

// Pod 에서 사용중인 IP 주소 확인 가능
kubectl get po –o wide
```   

***

#### 접속 확인
```
kubectl exec -it kuserver -- bash
```   
   
***

####  Pod 유지 개수 변경
* Replicaset 생성 후 Pod의 유지 개수를 변경해야 하는 경우
* spec.replicas 속성 값만 변경해 주면 됨
* Yaml 파일 수정, kubectl edit/kubectl patch 명령어 사용 등
   
```
kubectl apply -f d:\KubeTestWeb\kuweb-replicaset.yaml

// 변경된 정보 확인
kubectl get rs

kubectl get po
```
   
***
   
#### Pod 오류 시 자동 재 생성
* 장애가 발생하거나 필요에 의해 특정 Pod를 사용할 수 없는 경우 유 지 개수에 맞게 자동으로 재생성
   
```
// 특정 Pod 수동 삭제(Pod 목록에서 임의로 1개 선택)
kubectl delete po kuweb-replicaset-4jppw
```
   
***

#### ReplicaSet 삭제
```
kubectl delete rs <rs명 | -l label | --all> [옵션]

kubectl delete rs kuweb-replicaset
```
   
Replicaset에 의해 성성된 Pod도 함께 삭제된다.
   
***

금요일이라 다행이라고 해야할지.   
Docker, Kubernetes 개념 잡기 너무 힘들다.   
허공에 대고 뭘 자꾸 하는 거 같은데 뭘 하는 건지..?ㅠㅠ   
   
***



---
layout: single
title: "Kubernetes - Deployment"
categories: ['Cloud']
---

#### Deployment
* ReplicaSet과 Pod의 배포 관리
* Pod 및 ReplicaSet에 대한 선언적 업데이트를 제공
* ReplicaSet의 상위 오브젝트
* 쿠버네티스에서 공식적으로 Deployment를 사용할 것을 권장

***

#### Deployment API 확인
```
kubctl api-resources
```   
   

***

#### Deployment Yaml 파일 작성
* Kind 외에 ReplicaSet 과 동일한 방식으로 생성
   
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kuweb-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: kuweb-label
  template:
    metadata:
      labels:
        app: kuweb-label
    spec:
      containers:
      - name: kuweb
        image: testweb:1.0
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
        ports:
        - containerPort: 8080
```   

***

#### Deployment 생성
```
kubectl apply -f <Yaml 파일 경로> [옵션]

kubectl apply -f d:\KubeTestWeb\kuweb-deployment.yaml
```   
   
#### Deployment 목록 확인
```
// 유지되는 Pod 개수 확인 가능
kubectl get deployments [옵션]

// replicaset의 Pod 선택기, 컨테이너이름, 이미지이름 확인 가능
// deploy : deployments 짧은 명령어
kubectl get deploy -o wide
```
   
***

#### Deployment 상세 정보 확인
```
kubectl describe deploy [옵션]

kubectl describe deploy kuweb-deployments
```   
   
***

#### Deployment로 생성된 ReplicaSet, Pod 정보 확인
* Pod명은 Deployment 이름+16진수 랜덤 값으로 자동 생성
* po : 명령어 pods
   
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

####  Deployment 업데이트
* 애플리케이션 업데이트 시 중단 없이 업데이트 가능
* 변경 사항을 Revision에 기록하여 필요한 경우 롤백(rollback) 가능
* yaml 파일 수정 후 build
   
vsCode에서 dockerfile 우클릭 > build image > testweb:2.0   
이렇게 빌드를 했다.   
   
***
   
#### Deployment 이미지 업데이트
   
```
kubectl set image deploy <Deployment이름> <컨테이너이름>=<이미지이름> --record=true

kubectl set image deploy kuweb-deployment kuweb=testweb:2.0 --record=true

// --record : 변경사항을 기록하여 해당 버전의 ReplicaSet을 보존
```
   
***

#### Deployment Rollout 기록 확인
* 변경된 사항은 Revision으로 기록
   
```
kubectl rollout history deploy [Deployment이름] [옵션]

kubectl rollout history deploy kuweb-deployment

// 세부 확인
kubectl rollout history deploy kuweb-deployment --revision=2
```
   
***

#### Deployment 롤백
* 배포가 안정적이지 않은 경우 안정적인 이전 버전으로 롤백
   
```
kubectl rollout undo deploy <deploy이름> [--to-revision=번호]

kubectl rollout undo deploy kuweb-deployment

// --to-revision을 생략하면 바로 이전 버전으로 롤백
```
   
***

#### Deployment 삭제
* Deployment에 의해 생성된 ReplicaSet, Pod도 같이 삭제됨
   
```
kubectl delete deploy <deploy명 | -l label | --all> [옵션]

kubectl delete deploy kuweb-deployment
```
   
***



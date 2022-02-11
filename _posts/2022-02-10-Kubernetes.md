---
layout: single
title: "Kubernetes"
categories: ['Cloud']
---

#### Kubernetes
* [공식 사이트]
* 표준으로 사용되고 있는 컨테이너 오케스트레이션 도구
    * 오케스트레이션 : 컨테이너의 배포, 관리, 확장, 네트워킹을 자동화
* 구글에서 2014년 오픈소스로 공개
* 여러 대의 도커 호스트를 하나의 클러스터로 만들어 줌
    * 클러스터 : 여러 대의 컴퓨터들이 연결되어 하나의 시스템처럼 동작하는 컴퓨터들의 집합
* 세부적인 기능을 더욱 폭넓게 제공하여 실제 서비스 운영 단계에서 가장 많이 쓰이고 있음
* 여러 서버의 자원을 클러스터링해 컨테이너를 배치하는 것이 핵심 기능
* 다른 오케스트레이션 툴 보다 다양한 지식을 필요로 함
   
***

#### 용도에 따른 분류
   
|용도|설치 프로그램|
|---|--------|
|개발|Minikube, Docker Desktop 내장 쿠버네티스|
|테스트 및 운영|Kops, Kubesparay, Kubeadm, EKS, GKE 등|   
   

***

#### 설치
* Docker Desktop으로 설치
   
***

#### 버전 확인
```
kubectl version

kubectl version --short
```   
   
***

#### 오브젝트 확인
* 오브젝트 : 쿠버네티스는 대부분의 리소스를 오브젝트로 관리
   
```
kubectl api-resources

kubectl explain [오브젝트명]
```   
   
***

#### Pod
* 쿠버네티스에서 컨테이너를 생성하고 관리할 수 있는 가장 작은 배고 단위
* 컨테이너를 실행하기 위한 환경
* 1개의 Pod는 1개의 이상의 컨테이너를 포함
    * 일반적으로 1개의 컨테이너를 생성하여 사용

***

#### Pod 생성
* kubectl 명령어로도 생성 가능하지만 일반적으로 Yaml 파일을 이용하여 생성하는 것을 권장
   
```
kubectl run <Pod명> --image=<이미지명> [옵션]
```   
   
***

#### Pod 목록 확인
* 각 Pod는 고유한 IP주소를 가짐
* 쿠버네티스가 재 기동되면 Pod가 새롭게 생성되면서 주소가 변경될 수 있음
   
```
kubectl get pods [옵션]
```   
   
#### Pod 상세 정보 확인
   
```
kubectl describe pods [옵션]
```   
   
***

#### Pod 컨테이너 명령 실행
   
```
kubectl exec <Pod명> [-c 컨테이너명] [옵션] -- 명령어 [args …]

// 외부에서 명령어 실행
// pwd : 현재 작업 경로를 출력해주는 명령어
kubectl exec kuweb1 -- pwd

// 컨테이너 내부에 접근해서 명령어 실행
// /bin/bash 쉘로 접근해서 명령어 실행 (종료 시 exit)
kubectl exec kuweb1 -it -- bash

```   
   
***

#### 접속 확인
* 쿠버네티스는 외부에서 접근하려면 서비스 오브젝트를 따로 생성 필요
* 내부에서 접속 테스트를 하기 위해 임시로 서버 설치 후 Curl 도구를 활용하여 테스트 진행
   
```
CentOS 리눅스 서버 설치
> kubectl run -it kuserver --image=centos:7

- 리눅스 내 Curl 도구 설치
# yum –y install curl

- 접속 확인
# curl <Pod IP주소>:8080
```   
   
*** 

#### Pod 사용하기
* 쿠버네티스에서 오브젝트를 생성하고 관리할 때 명령어보다는 Yaml 파일 사용을 권장
* 공백 두 개로 들여쓰기 표현
* 들여쓰기 기준으로 계층적 구조를 가짐
* (#) 기호를 주석으로 사용
* 대소문자 구분
   
***

#### Pods API 확인
   
```
kubctl api-resources
```
   
|컬럼명|설명|
|---|------|
|NAME API|이름|
|SHORTNAMES API|짧은 이름(명령어에서 짧은 이름으로 사용 가능)|
|APIVERSION API|버전|
|NAMESPACED|독립적인 서비스 환경을 갖는 영역인지 여부|
|KIND|쿠버네티스 리소스의 유형|   
   
***

#### Yaml 파일로 Pod 생성하기
* 실습 때는 vsCode 에서 yaml 파일 생성했음
    * 하위 설정 작성 시에는 2개의 스페이스로 구분(tab안 안 되지만 vsCode에서 알아서 처리해줌)
```
# kuweb-pod.yaml 파일 생성

apiVersion: v1
kind: Pod
metadata: 
  name: kuweb-pod
  labels:
    name: kuweb-label
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
        protocol: TCP
```
   
```
kubectl apply -f <Yaml 파일 경로> [옵션]

kubectl apply -f 
```
   
***

#### Pod 삭제
   
```
kubectl delete pods <Pod명 | -l label | --all> [옵션]
```   

***





[공식 사이트]: [https://kubernetes.io/]





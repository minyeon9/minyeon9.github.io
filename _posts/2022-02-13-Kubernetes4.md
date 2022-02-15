---
layout: single
title: "Kubernetes - Service"
categories: ['Cloud']
---

#### Service
* Pod 집합에서 실행 중인 애플리케이션을 네트워크 서비스로 노출하는 추상적인 방법
* Pods에 접근하기 위한 규칙을 정의
* 하나의 애플리케이션에 하나의 Pod만 사용하지 않고 Pod의 집합을 사용하는 경우 각 Pod는 고유의 IP 주소를 가지기 때문에 접근이 까다로움
* Deployment를 사용하는 경우 Pod는 동적으로 생성/소멸 될 수 있기 때문에 배포 중 동작되는 Pod의 IP 주소는 변경될 수 있음
   
***

#### Service Type
   
|Type|설명|
|----|-------|
|ClusterIP|클러스터 내부 IP에 서비스를 노출. 클러스터 내에서만 서비스에 접근 가능. 외부로 Pods를 노출하지 않음. 기본 ServiceType|
|NodePort|Pods에 접근할 수 있는 Port를 클러스터의 모든 Node에 동일하게 개방. 외부에서 서비스에 접근 가능. ClusterIP 서비스가 자동으로 같이 생성됨. 접근 Port는 기본 랜덤 하게 지정됨. 특정 Port로 접근하도록 설정 가능||LoadBalancer|클라우드 공급자의 로드 밸런서를 사용하여 서비스를 외부에 노출. 외부에서 서비스에 접근 가능. 클라우드 환경에서만 사용 가능. NodePort 및 ClusterIP 서비스가 자동으로 같이 생성됨|
   
***

#### Service API 확인
   
```
kubctl api-resources
```
   
***

#### Service 연결할 Deployment 생성
* kuweb-deployment.yaml 파일 생성
   
***

#### Service 연결할 Deployment 생성
   
```
kubectl apply -f d:\KubeTestWeb\kuweb-deployment.yaml
```
   
-
   
```
kubectl get op -o wide
```
   
생성된 Pods 확인. 이건 명령어가 같아서 계속 나오넹..ㅎㅎ
   
***

#### Service Yaml 파일 작성
* 이번에도 마찬가지로 vsCode에서 작성했다.
* Name – Port 이름
* targetPort – Pods에서 사용중인 Port
* port – 추상화된 서비스 Port 지정
* nodePort – 외부에서 연결할 Port 지정
   
```
apiVaersion: v1
kind: Service
metadata:
  name: kuweb-service
sepc:
  type: NodePort
  selector:
    app: kuweb-label
  ports:
  - name: kuweb-port
    targetPort: 8080
    port: 80
    nodePort: 30000
```   
   
***

#### Service 생성
* 이것도.. deployment 명령어랑 동일
   
```
kubectl apply -f <Yaml 파일 경로> [옵션]

kubectl apply -f d:\KubeTestWeb\kuweb-serivce.yaml
```
   
***

#### Service 목록 확인
   
```
kubectl get services [옵션]
```   
   
-
   
```
// 유지되는 Pod 개수 확인
kubectl get svc -o wide
```
   
***

#### Service 상세 정보 확인
   
```
kubectl describe svc [옵션]

kubectl describe svc kuweb-service
```

***

#### Service 삭제
   
```
kubectl delete svc <svc명 | -l label | --all> [옵션]

kubectl delete svc kuweb-service
```
   
***

역시 명령어는 비슷해서 잊어버리더라도 검색해보면 되지만..   
개념을 모르면 힘들 거 같다.   
교재에 개념 설명이 되어 있으니 그걸 봐야겠다.   
   
***





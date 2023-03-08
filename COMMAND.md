## kubernetes work

#### 쿠버네티스 주요 오브젝트
1. Pod: 컨테이너를 다루는 기분 단위
2. Replica set: 컨테이너 집합을 관리하는 컨트롤러
3. Service: 포드에 접근하기 위한 규칙을 정의
4. Deployment: 어플리케이션을 배포 및 관리 


쿠버네티스에서는 오브젝트의 범위가 폭넓고 세밀한 단위로 사용된다.logs

쿠버네티스 노드의 역할은 마스터와 워커로 나뉜다.

#### 명령어
```
#쿠버네티스 정보 조회
$ kubectl config get-contexts

#오브젝트 목록 조회
$ kubectl api-resources

#포드 생성
$ kubectl apply -f nginx-pod.yml

#포드 목록 조회
$ kubectl get pods

#오브젝트 상세조회
$ kubectl describe <object> <object-name>
$ kubectl describe pods my-nginx-pod

*상세 정보에 IP 정보가 노출되지만 해당 IP 정보는 컨테이너 내부에서만 접근할 수 있는 IP 주소이다.
클러스터 외부에서 접근하기 위해선 NodePort 타입 서비스에서 접근할 수 있다*
내부에서 접근하여 nginx를 확인하려면 임시 노드를 생성 또는 쿠버네티스 클러스터의 노드에 접속하여 curl로 확인할 수 있다.
$ kubectl exec -it my-nginx-pod -- bash
$ kubectl run -i --tty --rm debug --image=alicek106/ubuntu:curl --restart=Never -- bash (임시 포드)
$ curl {ip}

#쿠버네티스 오브젝트 삭제
$ kubectl delete -f nginx-pod.xml
$ kubectl delete pods my-nginx-pod

#service 조회
$ kubectl get services
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   12d

```



### 포드 사용이유
docker가 아닌 포드를 사용하는 이유 중 하나는 여러 리눅스 네임스페이스를 공유하는 여러 컨테이너들을 추상화된 집합으로 사용하기 위해서다.
포드는 여러개의 컨테이너를 추상화해서 하나의 어플리케이션으로 동작하도록 만드는 훌륭한 컨테이너 묶음

pause 컨테이너는 네임스페이스를 공유하기 위한 컨테이너이다. 포드별로 생성된다.



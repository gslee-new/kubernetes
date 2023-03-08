## kubernetes work

#### 쿠버네티스 주요 오브젝트
1. Pod: 컨테이너를 다루는 기분 단위
2. Replica set: 컨테이너 집합을 관리하는 컨트롤러
3. Service: 포드에 접근하기 위한 규칙을 정의
4. Deployment: 어플리케이션을 배포 및 관리 


쿠버네티스에서는 오브젝트의 범위가 폭넓고 세밀한 단위로 사용된다.logs

쿠버네티스 노드의 역할은 마스터와 워커로 나뉜다.

##### 명령어
```
#포드 생성
kubectl apply -f nginx-pod.yml
#포드 목록 조회
kubectl get pods
#오브젝트 상세조회
kubectl describe <object> <object-name>
kubectl describe pods my-nginx-pod
```



3. kubectl get pods 
- object 목록 확인
4. kubectl describe pods <pods 이름>
- 포드 상세 정보 조회
네트워크가 고립되어서 접근은 불가하다. 80포트를 확인하기 위해서 쿠베 컨테이너로 접속해서 확인할 수 있다.
5. kubectl exec -it my-nginx-pod -- bash
6. curl 명령을 통해서 describe에서 확인한 url로 접근해보라
7. kubectl delete -f nginx-pod.yml
쿠버네티스 오브젝트 삭제 명령

# service 조회
$ kubectl get services
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   12d

포드는 컨테이너 ip주소를 가지고 있어 쿠버네티스 클러스터 내부에서 접근할 수 있고 kubectl exec 명령으로 포드 컨테이너 내부로 접속하며,
 logs 명령을 통해서 로그를 확인할 수 있다.

docker가 아닌 포드를 사용하는 이유 중 하나는 여러 리눅스 네임스페이스를 공유하는 여러 컨테이너들을 추상화된 집합으로 사용하기 위해서다.
무슨 말이냐 이 개념으로 포드를 이해하기는 너무나 어렵구나

pause 컨테이너는 네임스페이스를 공유하기위해서 포드별로 생성되는 컨테이너고 포드생성시 자동으로 생성된다.

포드는 여러개의 컨테이너를 추상화해서 하나의 어플리케이션으로 동작하도록 만드는 훌륭한 컨테이너 묶음

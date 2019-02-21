## 쿠버네티스란?

- 쿠버네티스를 가리키는 말은 여러가지가 있다.
	- 컨테이너 플랫폼
    	- 유명한 컨테이너 플랫폼으로는 Docker가 있다.
    - 마이크로서비스 플랫폼
    - 이식성 있는 클라우드 플랫폼 그리고 더 많은 기능...


## 컨테이너와 vm의 차이는?
- Container의 특징
	- vm은 container보다 훨씬 더 강력하게 격리된다. 
    	- vm은 가상화된 하드웨어 위에 os가 올라가는 형태로 거의 완벽하게 host와 분리
        - 반면 container는 os 가상화이다
        	- os 부분을 가상화해서 올리고 커널을 host와 공유
            - vm보다 얕게 격리된다.
- Container의 장점
	- 작다.
    	- 아키텍쳐 구조 참조 : https://cdn-images-1.medium.com/max/1600/1*wOBkzBpi1Hl9Nr__Jszplg.png
        - vm은 hypervisor가 hadrdware 가상화를 한 뒤에 Guest OS가 올라간다.
        - container는 Docker Engine 위에 application 실행에 필요한 바이너리만 올라간다.
        	- 그 외 커널 부분은 호스트의 커널을 공유
            	- 만약 호스트의 커널과 container의 커널이 다르다면? 다른 부분만큼만 패키징된다.
                	- 그만큼 공간을 절약 가능
    - 빠르다.
    	- host 머신보다 느리지만 vm과 비교하면 상대적으로 매우 빠르다.
        - vm은 io가 발생하는 통로가 container보다 많다.
        	- vm은 host os에서 거의 완전히 분리된 형태로 운영되지만 io가 오갈 때는 host os를  결국 병목이 발생할 수 밖에 없다.


## Docker의 특징
- 컨테이너 중 하나.
- Docker만의 문법으로 작성하여야 한다.
- 배포할 어플리케이션의 설치 과정을 상세히 기술해야 한다.
- 의존성에 필요한 것이 있다면 알아서 설치해준다.
- DB를 외부에 마운트해서 연동 가능.
	- 시스템이 아무리 변경된다고 해도 DB는 영향을 받지 않는다.
- 네트웍은 분리 가능하고 원한다면 host로 통신도 가능하다.
- Light and Scalable.

## Docker 실습
- Dockerfile을 작성
	- Docker문법을 이용해야 한다.
	```
    FROM PYTHON:2
    	...
    ```
- 실행 방법
	- docker run -d --name 도커 이름 -e 환경변수...
- 로그 보기
	- docker logs -f 도커 이름

## 쿠버네티스란?
- Kubernetes는 사실상의 컨테이너 관리 표준
- 컨테이너를 효과적으로 배포할 수 있는 툴
	- container 자체를 묶으면 너무 low level로 묶이기 때문에 pod을 이용
	- 여러 개의 컨테이너는 하나의 Pod이라는 단위로 묶음
    	- Pod 내에서 컨테이너들은 IP와 스토리지를 공유
- Kubernetes가 없는 컨테이너 환경
	- 각 컨테이너가 독립적으로 실행
    - 각자 다른 IP/NETWORK로 통신
    - 서로 다른 노드에 설치될 수도 있음
    - 컨테이너끼리 디스크 자원을 공유할 수 없음
- Kubernetes 아키텍쳐
	- Kubernetes Master가 Kubernetes Node들을 관리
    - Kubernetes Node는
    	- 여러 개의 Pod을 갖고 있음
        - Kubelet을 갖고 있음
        	- Master의 API Server와 통신
        - cAdvisor를 갖고 있음
    	- Kube-Proxy를 갖고 있음
        	- Pod들간의 통신을 할 때 컨테이너 이름을 기준으로 통신을 할 수 있게 해줌
	- Kubernetes Master는
    	- API Server를 갖고 있음
        	- Controller Manager를 갖고 있음
            - Scheduler를 갖고 있음
        - etcd를 갖고 있음
        	- 모든 메타정보를 갖고 있음
- Kubernetes Service
	- Service 
    	- L4 로드밸런서로 로드밸런싱 및 페일오버
    		- ex) 여러개의 접속이 들어왔을 때 어느 pod으로 갈지...
            - L4는 포트 기반으로 서비스를 나눠줌
    - Service는 MSA상의 서비스와 거의 동일한 단위
- Kubernetes Ingress
	- Ingress
    	- L7 로드밸런서	
        	- L7은 L4와 달리 패킷의 내용을 볼 수 있음
        - URI 기반으로 서비스 별 라우팅
        - 서비스 앞 단에 위치
        	- 하나의 Ingress는 많은 서비스를 관리
		- Google Cloud의 로드밸런서
- Kubernetes Deployment & ReplicaSet
	- Deployment가 복수 개의 ReplicaSet을 통해 Rolling Update 처리
    	- 테스트용 프로그램을 Deployment에 올려본다.
        - 성공하면 ReplicaSet -> Pod -> Service -> Ingress으로 순차적으로 배포
        	- 운영시스템의 안정성을 높임
	- ReplicaSet에서 Pod들의 Scaling 담당
- Kubernetes Namespace
	- Kubernates 클러스터를 부서, 프로젝트 등의 단위로 분리
    - 리소스를 분리하여 관리
    	- 물리적으로 완전히 분리
        - 리소스를 더 많이 더 적게 주는 것이 가능
        - 하나의 쿠버네티스를 나눠쓰고 싶을 때

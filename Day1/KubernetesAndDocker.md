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
- 설치 과정을 상세히 기술해야 한다.
- Docker만의 문법으로 작성하여야 한다.
- 의존성에 필요한 것이 있다면 알아서 설치해준다.
- DB를 외부에 마운트해서 연동 가능.
	- 시스템이 아무리 변경된다고 해도 DB는 영향을 받지 않는다.
- 네트웍은 분리 가능하고 원한다면 host로 통신도 가능하다.
- Light and Scalable

## 

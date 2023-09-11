# Docker and EKS 시작하기
- [Workshop 링크](https://catalog.us-east-1.prod.workshops.aws/workshops/46236689-b414-4db8-b5fc-8d2954f2d94a/ko-KR)

## 1. Cloud9 IDE 환경 구성
- 중요
  - Cloud9 인스턴스에 IAM 역할 업데이트 후에 **임시 자격 증명을 비활성화**하고 **기존에 존재하는 자격증명 파일을 제거**해야한다. => 안 하면 EKS가 제대로 생성되지 않는다. (IAM 2개가 충돌?)
  -  증상 :
    - Cloud9 콘솔에서 리소스가 이미 존재한다는 오류가 발생하고, CloudFormation과 AWS EKS에서는 제대로 생성된 것으로 보이나 kubectl을 실행하였을 때 ```The connection to the server localhost:8080 was refused - did you specify the right host or port?``` 메시지가 출력됨.([stack overflow 방법-확인 안 해봄](https://stackoverflow.com/questions/51121136/the-connection-to-the-server-localhost8080-was-refused-did-you-specify-the-ri))
  - 방법 :
    - Cloud9 콘솔에서 우상단 톱니바퀴 버튼을 누르고, AWS Settings 메뉴에 들어가서 Credentials에서 AWS managed temporary credentials의 토글 스위치를 클릭하여 x 표시로 변경한다.
![image](https://github.com/Mu-jun/TIL/assets/98201978/b171cded-b778-48d7-a004-78b91cf920dc)
    - 다음 명령얼르 실행하여 기존에 존재하는 자격증명 파일을 제거할 수 있다.
```
rm -vf ${HOME}/.aws/credentials
```

## 2. Docker
### 기본 명령어
- Docker 이미지 검색
```
docker search [검색어]
```

- Docker 이미지 다운로드
```
docker pull [Docker 이미지명]
```

- 로컬의 Docker 이미지 목록
```
docker images
```

- Docker 이미지 삭제
```
docker rmi [Docker 이미지명]
```

- Docker 실행
```
docker run --name [컨테이너의 이름] -d -p 80:80 [Docker 이미지명]
또는
docker run --name [컨테이너의 이름] -dp 80:80 [Docker 이미지명]
```
-d => 백그라운드에서 실행  
-p 머신port번호:컨테이너port번호 => 머신port번호로 접근하면 컨테이너의 80번 포트로 연결하라는 포트를 매핑하는 옵션  

- 컨테이너 목록 확인
```
docker ps  # 실행중인 컨테이너만 확인가능
docker ps  -a  # 모든 컨테이너(실행, 정지) 확인가능
```

- 컨테이너 정지
```
docker stop [컨테이너 이름]
```

- 정지된 컨테이너 재실행
```
docker start [컨테이너 이름]
```

- 정지된 컨테이너 삭제
```
docker rm [컨테이너 이름]
```

- 강제로 모든 컨테이너 삭제
```
docker rm -f $(docker ps -aq)
```

- 강제로 모든 Docker 이미지 삭제
```
docker rmi -f $(docker images -q)
```

### Docker 이미지 build
- [Dockerfile 참조](https://docs.docker.com/engine/reference/builder/)

## 3. EKS
### kubectl 기본 명령어
- 버전 확인
```
kubectl version --short=ture
```

- Kubernetes Object의 종류와 단축명 등을 확인
```
kubectl api-resources
```

- 생성된 Object 확인
```
kubectl get [Object명 또는 단축명]

# ,를 사용하여 여러 objcet를 한번에 확인가능
kubectl get [Object명 또는 단축명],[Object명 또는 단축명],...

# -w 옵션을 사용하면 object를 모니터링한다.
kubectl get replicaset -w
```

- yaml을 통한 선언형 배포
```
kubectl apply -f [yaml 파일명]
```

- 롤백
```
kubectl rollout undo [object 종류] [metadata의 name]
```

- Tip
  - Namespace를 이용하여 자원 나누어 좀더 편하게 관리할 수 있다.

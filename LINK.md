### 실습용 Github Repository
```
https://github.com/MangDan/cloud-native-devops-workshop-wercker-oke
```

### OCI 접속 주소
```
https://console.ap-seoul-1.oraclecloud.com/?tenant=<각 회사별 테넌트명>&provider=OracleIdentityCloudService
```

### SSH 공개키(Public Key)
```
https://raw.githubusercontent.com/MangDan/cloud-native-devops-workshop-wercker-oke/master/sshkey/id_rsa.pub
```

### SSH Putty 개인키(Private Key)
```
https://raw.githubusercontent.com/MangDan/cloud-native-devops-workshop-wercker-oke/master/sshkey/id_rsa.ppk
```

### SSH OpenSSH 개인키(Private Key)
```
https://raw.githubusercontent.com/MangDan/cloud-native-devops-workshop-wercker-oke/master/sshkey/id_rsa
```

### SSH OpenSSH 개인키(Private Key)
```
https://raw.githubusercontent.com/MangDan/cloud-native-devops-workshop-wercker-oke/master/sshkey/id_rsa
```

### 도커 설치
```
# 도커 설치
sudo yum install docker-engine

# 도커 서비스 활성화
sudo systemctl enable docker

# 도커 서비스 시작
sudo systemctl start docker

# 도커 설치 확인
sudo docker -v
```

### Git 설치
```
# Git 설치
sudo yum install git-core

# Git 설치 확인
git --version
```

### oci-cli 설치
```
# oci-cli 설치
bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"
```

```
===> In what directory would you like to place the install? (leave blank to use '/home/opc/lib/oracle-cli'): <엔터>

===> In what directory would you like to place the 'oci' executable? (leave blank to use '/home/opc/bin'): <엔터>

===> In what directory would you like to place the OCI scripts? (leave blank to use '/home/opc/bin/oci-cli-scripts'): <엔터>

===> Currently supported optional packages are: ['db (will install cx_Oracle)']
What optional CLI packages would you like to be installed (comma separated names; press enter if you don't need any optional packages)?:
 <엔터>

===> Modify profile to update your $PATH and enable shell/tab completion now? (Y/n): <Y>

===> Enter a path to an rc file to update (leave blank to use '/home/opc/.bashrc'): <엔터>
```

```
# oci-cli 설치 확인
oci -v
```

### oci-cli 구성
```
oci setup config
```

```
Enter a location for your config [/home/opc/.oci/config]: <엔터>
Enter a user OCID: <OCI Console에서 획득, 가이드 참조>
Enter a tenancy OCID: <OCI Console에서 획득, 가이드 참조>
Enter a region: ap-seoul-1
Do you want to generate a new RSA key pair? (If you decline you will be asked to supply the path to an existing key.) [Y/n]: Y
Enter a directory for your keys to be created [/home/opc/.oci]: <엔터>
Enter a name for your key [oci_api_key]: <엔터>
Enter a passphrase for your private key (empty for no passphrase): <엔터>
```

### kubectl
```
# kubectl 설치
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl

# kubectl 실행 권한 설정
chmod +x ./kubectl

# kubectl 실행 패스에 추가
sudo mv ./kubectl /usr/local/bin/kubectl

# kubectl 설치 확인
kubectl version
```

### 프로퍼티스 파일 열기 (.properties)
```
# 마이크로 프로파일
vi ~/cloud-native-devops-workshop-wercker-oke/helidon-movie-api-mp/src/main/resources/META-INF/microprofile-config.properties

# 스프링부트 프로파일
vi ~/cloud-native-devops-workshop-wercker-oke/springboot-movie-people-api/src/main/resources/application-oracle.properties
```

### Github 소스 반영
```
cd ~/cloud-native-devops-workshop-wercker-oke

# 변경 소스 추가
git add .

# 변경 소스 커밋
git commit -m "hi"

# 변경 소스 깃헙 푸시
git push -u origin master
```

### 도커 이미지 빌드, 레지스트리 푸시
```
# 서비스 프로젝트로 이동
cd ~/cloud-native-devops-workshop-wercker-oke/helidon-movie-api-mp

# 이미지 빌드
sudo docker build --tag icn.ocir.io/apackrsct01/movie-api-service-<이름 이니셜>:latest .

# 도커 이미지 확인
sudo docker image ls

# 도커 이미지를 레지스트리에 푸시
sudo docker push icn.ocir.io/apackrsct01/movie-api-service-<이름 이니셜>:latest
```

### 쿠버네티스 네임스페이스(namespace), 시크릿(secret) 생성
```
# 네임스페이스 생성
kubectl create namespace <namespace>

# 시크릿 생성
kubectl create secret docker-registry ocirsecret --docker-server=icn.ocir.io --docker-username='<tenancy-namespace>/oracleidentitycloudservice/<username>' --docker-password='<Auth Token>' --namespace=<namespace>
```

### 쿠버네티스 YAML 파일 수정
```
vi ~/cloud-native-devops-workshop-wercker-oke/helidon-movie-api-mp/app.yaml
```

### 쿠버네티스에 YAML 적용
```
# yaml 파일의 오브젝트 상태 적용
kubectl apply -f ~/cloud-native-devops-workshop-wercker-oke/helidon-movie-api-mp/app.yaml

# 서비스와 파드 목록 확인
kubectl get all --namespace <namespace>
```

### UI에서 마이크로서비스의 주소 변경
```
vi ~/cloud-native-devops-workshop-wercker-oke/jet-movie-msa-ui/src/js/endpoints.json
```
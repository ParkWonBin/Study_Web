# 서버 만들어 웹 호스팅하기

## 1. 무료로 서버 호스팅하는 곳 찾기
##### 추천 : 오라클 클라우드 
스팩 : Free Tier(OCPU, 램1GB, 인스턴스 2개 부트볼륨 각각 50GB, 총 100GB)  
주의 : 인스턴스 만들 때 Volum 50GB 이하로 제한할 것  

## 2. 오라클 클라우드 가입 및 로그인
##### 아마존은 ID, PW 뿐만아니라 약식 이름까지 key로 넣어야한다. 
참고 : [오라클 클라우드 가입][오라클 클라우드 가입]  
2.1  로그인 > 약식 이름 : {가입 시 입력한 약식 이름 : pwb1128}  
2.2. 로그인 > 계정 이름 : {가입 시 입력한 Email : pwb1128@*****}  
2.3. 로그인 > 비밀 번호 : {가입 시 입력한 PW}  

## 3. VCN 네트워크 생성
##### 오라클 클라우드 가입 후 일정 시간 기다리면 VCN 생성 버튼 생김
참고 : [VCN 생성][오라클 클라우드 VCN 생성]  


## 4. SSH 생성 및 Putty에 서버 연결
##### PuTTY는 SSH생성 및 서버 연결에 쓰인다.
참고 : [PuTTY - SSH 생성 및 서버 연결]  
참고 : [PuTTY - 다운로드]  
주의사항 : SSH 생성 시 ID/PW 설정 확인 - 서버의 admin계정의 ID/PW가 됩니다.

## 5. 인스턴스 생성 
##### 생성 과정에서 컴퓨터 운영체제, SSH 설정 등..
참고 : [인스턴스 생성][오라클 클라우드 인스턴스 생성]  
5.1. 운영체제 종류 및 버전 선택하기 (플라스크 사용시 ubuntu 20.4 추천)  
5.2. SSH 등록 : (PuTTyGen 통해 생성, ID PW 설정값이 해당 서버의 admin ID/PW가 된다.)  
5.3. SSH,OS Image 설정을 잘못한 경우 해당 인스턴스를 삭제 후 다시 만들어야 합니다. 주의.  
5.4. 인스턴스 생성 시 Volum 제한 50GB로 설정 할 것  

## 6. 인스턴스 고정 IP 설정 및 포트 개방
- 참고 : [고정 IP 설정하기][오라클 클라우드 고정 IP 설정]
- 참고 : [포트 개방하기][오라클 클라우드 포트 개방]

## 7. 인스턴스에 도메인 연결
- 참고 : [DNS 구매 - GoDaddy][GoDaddy_URL]
- 참고 : [DNS 구매 후 오라클 서버에 적용][인스턴스에 도메인 연결]
  
7.1. GoDadday에서 이메일 인증 안하면 ns(네임서버) 설정 중 오류 발생할 수 있음
7.2. GoDaddy > 내제품 > 도메인 메뉴 > DNS 관리  >  네임서버 변경 > 내 자신의 네임서버 입력(고급)  
7.3. 오라클 클라우드 > DNS ZONE > Nameservers 확인  

## 8. PuTTY - 오라클 클라우드 서버 접속하기
- 참고 : [오라클 클라우드 서버 접속][오라클 클라우드 서버 접속]  

8.1. PuTTY > SSH > Auth 파일 설정
8.2. PuTTY > Session > IP,Port 저장 > 해당 세션 더블클릭

비고1 : 관리자 계정으로 로그인 시 Login As 위치에 "ubuntu" 입력  
비고2 : 관리자 계정의 ID/PW는 SSH 생성 시 설정했던 ID/PW 입니다.  
비고3 : PW 입력 시 화면변화 없으니 주의. (키보드 눌려도 *로 글자수 표시되지 않음)  


## 9. 서버 내 계정 생성 및 권한 부여
참고1 : [인스턴스에 사용자 추가][Linux 인스턴스 사용자 추가]
참고2 : [ubuntu 사용자 root 권한 주기][사용자 권한 주기]
참고3 : [SSH key 추가로 로그인][리눅스 SSH key 추가로 로그인]
참고4 : [PuTTY 자동로그인 설정][PuTTY 자동로그인 설정]
참고5 : [VIM 사용법][vim 사용법]

```shell
# 1. 계정생성
$ sudo userdel new_user # 유저 삭제
$ sudo adduser new_user # 입력 후 PW 설정 필요
$ sudo adduser new_user --disabled-password # PW 없이 추가
# PW 입력 시 타이핑 해도 화면에 글자수 맞게 * 생기지 않음.

# 2. root 권한 부여
$ sudo vim /etc/sudoers
# 편집모드 진입 : 방향키로 커서 이동후 (단축키 a,i,o)
# 편집모드 탈출 : esc 
# vi/vim 탈출  : ":wq!" 입력

# 3. 서버에서 SSH 생성
$ sudo su - new_user 
$ ssh-keygen -t rsa 
# 여기서 passphrase 는 공란으로 설정한다. 
# 패스워드 보다 SSH 파일 소유 여부로 로그인하는 게 보안성이 높기 때문

$ cd ../home/new_user/.ssh && ls -al 
# ls 옵션 = {a:숨김파일 포함, l: 내용 자세히, ...}
# 해당 경로에 파일 id_rsa, id_rsa.pub 파일 생성된 것 확인

#4. 해당 SSH 로컬로 출력(참고5)
$ mv id_rsa.pub authorized_keys # 파일명 변경
$ cat id_rsa # 파일 수정 => 내용 보기 목적
# id_rsa의 내용을 그대로 복사하여 로컬pc 경로에 확장자 없음으로 저장
# PuTTY gen 통해서 읽어와서 private key로 저장 SSH(.ppk)

#5. PuTTY로 로그인 연결
# 5.1. Session > Host Name에 IP 대신 도메인만 입력 (wbpark.info)
# 5.2. Connection > Data > Auto-login username = (new_user)
# 5.3. Connection > SSH > Auth > [Browse] > SSH(.ppk) 연결
# 5.4. Session > Saved Sessions = 이름 입력 > Save
# SSH(.ppk) 파일만 있으면 해당 도메인에 user id 페스워드 없이 로그인 가능
```

## 10. VSCode로 PuTTY 연동해서 사용하기
참고  : [Could not establish connection](https://kkkapuq.tistory.com/108)
VSCode 확장 : "Remot - development"

10.1. 원격 탐색기에 도메인 입력
VSCode 리본 > SSH Targets [+] 버튼 클릭 > IP 입력 (wbpark@wbpark.info)

10.2. config 위치 설정
SSH Targets [톱니바퀴] > C:\Users\pwb1128\.ssh\config

10.3. config 파일 수정
SSH Targets [톱니바퀴] > .../config 클릭 > 파일 수정
```SSHConfig
Host wbpark.info
  HostName wbpark.info
  User wbpark
  IdentityFile C:\Users\pwb1128\.ssh\wbpark_wbpark
```
10.4 key 변환
10.4 PuTTYgen > Load (기존에 SSH(.ppk) 파일 읽어오기) > Conversions > Export OpenSSH key > 해당 config 파일 있는 위치에 확장자 표시 없이 "모든파일"로 저장 (10.3에 IdentityFile 경로/파일명과 일치)

10.5 Error > Could not establish connection
만약 연결 중에 에러가 발생하면 config 경로에서 known... 으로 생성된 파일 존재 시 삭제 진행할 것


## 11. PuTTY - Flask 설치 
- 참고 : [오라클 클라우드 Ubuntu 20.04 인스턴스 기본 설정](https://www.wsgvet.com/cloud/6)
- 참고 : [서버에 Flask 설치하기][서버에 Flask 설치하기]


```shell
## 업데이트
$ sudo apt update -y
$ sudo apt-get update
$ sudo apt-get upgrade

## 파이썬 개발환경 만들기
$  python3 --version
$ sudo apt install build-essential python3-pip libffi-dev python3-dev python3-setuptools libssl-dev
$ sudo apt install python3-venv

## 서버 내 폴더구조 만들기 
$ mkdir proj && cd proj
$ mkdir ProjectName && cd ProjectName

## 해당 폴더 내 가상환경 설치 및 실행
$ python3 -m venv venv
$ source venv/bin/activate

## 플라스크 설치
$ pip3 install flask
```

#### 레퍼런스 및 부연설명
```shell 
# 키워드 이름 뜻 설명
sudo : Supper User Do
su : Switch User
chmod : Change Mode
vi : Visual editor
vim : vi + important
ls : list segments
cd : change Directory
mv : move(파일 위치 변경, 파일명 변경)
cat : concatenate (내용 이어서 쓰기)
```

```text
chmod 관련 권한 코드 : 
[ 읽기(r), 쓰기(w), 실행(x) ] 을 이진수로 표현 후 십진수로 변환
[ 소유자, 구룹, 기타 ]에 대해서 해당 코드를 반복

ex ) 소유자 모든권한, 구룹과 기타는 권한 전혀 없음의 경우
111 => 7, 000 => 0 이므로 해당 코드는 700이 된다. 
```

참고: [리눅스 700 권한 관련][리눅스 권한관련]


[Flask 웹서버 구동][init_Flask]

[서버에 Flask 설치하기]:https://ko.linux-console.net/?p=388
[GoDaddy_URL]:https://kr.godaddy.com/
[init_Flask]:https://velog.io/@poiuyy0420/파이썬-Flask-웹서버-구동하기
[오라클 클라우드 가입]:https://technfin.tistory.com/entry/%EC%98%A4%EB%9D%BC%ED%81%B4-%ED%81%B4%EB%9D%BC%EC%9A%B0%EB%93%9C-%EB%AC%B4%EB%A3%8C-%EA%B0%80%EC%9E%85-%EC%98%A4%EB%A5%98-%EB%B0%8F-%EC%A3%BC%EC%9D%98%EC%82%AC%ED%95%AD
[오라클 클라우드 인스턴스 생성]:https://technfin.tistory.com/entry/%EC%98%A4%EB%9D%BC%ED%81%B4-%ED%81%B4%EB%9D%BC%EC%9A%B0%EB%93%9C-%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4-%EC%83%9D%EC%84%B1-%EC%84%9C%EB%B2%84-%EB%A7%8C%EB%93%A4%EA%B8%B0?category=867921
[오라클 클라우드 고정 IP 설정]:https://technfin.tistory.com/entry/%EC%98%A4%EB%9D%BC%ED%81%B4-%ED%81%B4%EB%9D%BC%EC%9A%B0%EB%93%9C-%EA%B3%A0%EC%A0%95IP-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0?category=867921
[오라클 클라우드 포트 개방]:https://technfin.tistory.com/entry/%EC%98%A4%EB%9D%BC%ED%81%B4-%ED%81%B4%EB%9D%BC%EC%9A%B0%EB%93%9C-%ED%8F%AC%ED%8A%B8-%EA%B0%9C%EB%B0%A9%ED%95%98%EA%B8%B0?category=867921
[오라클 클라우드 서버 접속]:https://technfin.tistory.com/entry/%EC%98%A4%EB%9D%BC%ED%81%B4-%ED%81%B4%EB%9D%BC%EC%9A%B0%EB%93%9C-%EC%84%9C%EB%B2%84-%EC%A0%91%EC%86%8D%ED%95%98%EA%B8%B0-PuTTY?category=867921
[오라클 클라우드 VCN 생성]:https://blogger.pe.kr/915?category=144028
[인스턴스에 도메인 연결]:https://blog.naver.com/bb_/222167412684
[PuTTY - SSH 생성]:https://itreport.tistory.com/603
[PuTTY - 다운로드]:https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
[PuTTY - SSH 생성 및 서버 연결]:https://itreport.tistory.com/603
[Linux 인스턴스 사용자 추가]:https://aws.amazon.com/ko/premiumsupport/knowledge-center/new-user-accounts-linux-instance/
[사용자 권한 주기]:https://kbs4674.tistory.com/134
[vim 사용법]:https://www.morenice.kr/25
[리눅스 권한관련]:https://kbs4674.tistory.com/134
[리눅스 SSH key 추가로 로그인]:https://technfin.tistory.com/entry/%EB%A6%AC%EB%88%85%EC%8A%A4-SSH-Key-%EC%B6%94%EA%B0%80%ED%95%98%EC%97%AC-%EC%82%AC%EC%9A%A9%EC%9E%90%EB%A1%9C-%EB%A1%9C%EA%B7%B8%EC%9D%B8%ED%95%98%EA%B8%B0-%EC%98%A4%EB%9D%BC%ED%81%B4-%EB%A6%AC%EB%88%85%EC%8A%A48
[PuTTY 자동로그인 설정]:http://www.fa-programmer.xyz/?p=710



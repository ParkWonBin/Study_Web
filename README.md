# 서버 만들어 웹 호스팅하기

## 1. 무료로 서버 호스팅하는 곳 찾기
##### 추천 : 오라클 클라우드 
스팩 : Free Tier(OCPU, 램1GB, 인스턴스 2개 부트볼륨 각각 50GB, 총 100GB)  
주의 : 인스턴스 만들 때 Volum 50GB 이하로 제한할 것  

## 2. 오라클 클라우드 가입 및 로그인
##### 아마존은 ID, PW 뿐만아니라 약식 이름까지 key로 넣어야한다. 
참고 : [오라클 클라우드 가입][오라클 클라우드 가입]  
- 약식 이름 : {가입 시 입력한 약식 이름 : pwb1128}  
- 계정 이름 : {가입 시 입력한 Email : pwb1128@*****}  
- 비밀 번호 : {가입 시 입력한 PW}  

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
주의1 : 운영체제 종류 및 버전 선택하기 (플라스크 사용시 ubuntu 20.4 추천)  
주의2 : SSH 등록 : (PuTTyGen 통해 생성, ID PW 설정값이 해당 서버의 admin ID/PW가 된다.)  
주의3 :  SSH,OS Image 설정을 잘못한 경우 해당 인스턴스를 삭제 후 다시 만들어야 합니다. 주의.  
주의4 :  인스턴스 생성 시 Volum 제한 50GB로 설정 할 것  

## 6. 인스턴스 고정 IP 설정 및 포트 개발
- 참고 : [고정 IP 설정하기][오라클 클라우드 고정 IP 설정]
- 참고 : [포트 개방하기][오라클 클라우드 포트 개방]

## 7. 인스턴스에 도메인 연결
- 참고 : [DNS 구매 - GoDaddy][GoDaddy_URL]
- 참고 : [DNS 구매 후 오라클 서버에 적용][인스턴스에 도메인 연결]
  
주의사항 : GoDadday에서 이메일 인증 안하면 ns(네임서버) 설정 중 오류 발생할 수 있음  
7.1. 오라클 클라우드 > DNS ZONE > Nameservers 확인  
7.2. GoDaddy > 내제품 > 도메인 메뉴 > DNS 관리  >  네임서버 변경 > 내 자신의 네임서버 입력(고급)  

## 8. PuTTY - 오라클 클라우드 서버 접속하기
- 참고 : [오라클 클라우드 서버 접속][오라클 클라우드 서버 접속]  

8.1 PuTTY > SSH > Auth 파일 설정
8.2 PuTTY > Session > IP,Port 저장 > 해당 세션 더블클릭

비고1 : 관리자 계정으로 로그인 시 Login As 위치에 "ubuntu" 입력    
비고2 : 관리자 계정의 ID/PW는 SSH 생성 시 설정했던 ID/PW 입니다.
비고3 : PW 입력 시 화면변화 없으니 주의. (키보드 누를 떄 *로 글자수 표시되지 않음)

## 9. PuTTY - Flask 설치 
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

#### 레퍼런스
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
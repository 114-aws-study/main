일일사 AWS스터디 핸즈온 2018-03-21
========

## 개요

일일사 AWS스터디 핸즈온(2018-03-21) 내용을 스크린캡쳐 한 자료임.

## 핸즈온 구성도
![구성도](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321001.png)

## 보안 그룹 생성

보안 그룹 설정 규칙은 크게 두종류의 규칙이 있음
* 외부로부터 들어오는 `인바운드`
* 내부로부터 내보내는 `아웃바운드`

아웃바운드는 운용룰에 따라 제한된 로그포트(Zabbix등?), 업데이트용 yum포트 개방하는 케이스가 있음

그룹명은 운용하게 쉽게 정해진 규칙에 따라 작성할것.
WebAP의 EC2 인스턴스 접속은 SSH터널링/우회서버를 작성하여 RDS및 EC2접속을 하는것이 바람직하나 핸즈온에서는 작업PC의 외부IP를 지정하여 접속


| 그룹명                | 유형          | 프로토콜  | 포트 범위 | 소스                               |
| ------------------- | ------------ | ------- | ------- | -------------------------------- |
| handson-elb-group   | HTTP         | TCP     | 80      | 0.0.0.0/0                        |
| handson-webap-group | HTTP         | TCP     | 80      | `handson-elb-group`의 보안 그룹ID   |
| handson-webap-group | HTTP         | TCP     | 22      | 작업PC의 외부IP설정                  |
| handson-rds-group   | MySQL/Aurora | TCP     | 3306    | `handson-webap-group`의 보안 그룹ID |

## 보안 그룹

![EC2의 보안 그룹 메뉴](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321002.png)
![ELB 보안 그룹 생성](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321003.png)
![ELB 보안 그룹 생성확인/그룹ID 복사](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321004.png)
![WebAP 보안 그룹 생성](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321005.png)
![RDS 보안 그룹 생성](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321006.png)

## WebAP

### 인스턴스 시작

![007](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321007.png)

### 인스턴스 선택
![008](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321008.png)

>아마존 리눅스 버전에 대해서
* Amazon Linux 2017.09.1
RHEL6계열이나 기존 RHEL에 비해 커널버전, 비교적 최신 패키지를 지원 아래의 RHEL7 릴리즈후 2년간 서포트
* Amazon Linux LTS Candidate 2017.12
RHEL7계열 - 현재Candidate 정식 릴리즈후 5년간 서포트

### 인스턴스 유형 선택

![009](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321009.png)

### 인스턴스 세부 정보 구성
![010](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321010.png)

>**종료 방지 기능 활성화:**  
인스턴스 종료(Terminate) 해도 완전삭제가 되지않고 정지(Stop)됨
오토스케일링에 의해 생성된 인스턴스에 이 옵션이 설정되어 있을경우 요금폭탄의 가능성이 있음

> **T2무제한:**  
T2인스턴스는 버스트 모델 채용으로 쌓아놓은 크레짓을 소모하면 성능저하의 가능성이 있음.
성능저하 구간에 대한 비용을 지불하여 제한없이 사용하는 옵션
[T2 무제한(Unlimited) 기능 – 피크에도 고성능 컴퓨팅 활용하기](https://aws.amazon.com/ko/blogs/korea/new-t2-unlimited-going-beyond-the-burst-with-high-performance/)

### 고급 세부 정보

![011](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321011.png)

```bash
#!/bin/bash
yum update -y
yum install -y nginx mysql56
chkconfig --level 345 nginx on
service nginx start
```

> 초기화 방법은 여러가지가 존재함.
* 쉘 스크립트를 직접입력하는 방법
* s3등 업로드 데이터를 다운로드 후 실행하는 방법
* 작업한 이미지를 사용하는 방법

### 스토리지 추가

![012](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321012.png)

### 태그 추가

![013](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321013.png)

### 보안 그룹 구성

![014](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321014.png)

### 인스턴스 시작 검토

![015](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321015.png)

### 기존 키 페어 선택 또는 새 키 페어 생성

![016](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321016.png)


### 시작 상태
![017](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321017.png)

### 확인: 퍼블릭IP

![018](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321018.png)

## RDS

### 인스턴스 작성

![020](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321020.png)

### 엔진 선택

![021](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321021.png)

### DB 세부 정보 지정

![022](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321022.png)

### 식별자, 마스터 사용자 이름, 마스터 암호 설정후 다음단계로

![023](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321023.png)

### 기존 VPC 보안 그룹 사용 설정

![024](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321024.png)

> 다중 AZ 옵션: 다른 AZ에 예비인스턴스를 구축해놓고 데이터 동기화
[Amazon RDS 다중 AZ 배포](https://aws.amazon.com/ko/rds/details/multi-az/)

![025](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321025.png)

![026](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321026.png)

### 인스턴스 시작(생성)

![027](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321027.png)


![028](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321028.png)

### 생성후 인스턴스

![029](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321029.png)

### 인스턴스 세부 정보 확인

![030](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321030.png)

### 엔드포인트 확인

![031](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321031.png)

## 로드밸런스

![032](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321032.png)
![033](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321033.png)
![034](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321034.png)
![035](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321035.png)
![036](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321036.png)
![037](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321037.png)
![038](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321038.png)
![039](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321039.png)
![040](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321040.png)
![041](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321041.png)
![042](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321042.png)

## WebAP RDS

 `~/.ssh/config` SSH접속 정보를 설정해 두면 편리

```
Host myaws
  HostName 13.115.86.144
  User ec2-user
  Port 22
  IdentityFile ~/.ssh/my-aws-20180321.pem
```

RDS 설정후 실행

```
mysql -u handson_rds -p \
-h handsonrds.cnxsiscwistl.ap-northeast-1.rds.amazonaws.com
```

![019](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321019.png)

## 브라우저 접속 확인

![043](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/58521a2327a279d8c8def9a6c5d289d95c73cb3a/20180321043.png)

### ELB CLB -> ALB 마이그레이션



![044](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/e47184f9a35801e607317fed8c5601f5966cfdf2/20180321044.png)

![045](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/e47184f9a35801e607317fed8c5601f5966cfdf2/20180321045.png)

![046](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/e47184f9a35801e607317fed8c5601f5966cfdf2/20180321046.png)

ALB는`로드밸런서`와`대상 그룹`으로 역할분담이 되어있음.

![047](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/e47184f9a35801e607317fed8c5601f5966cfdf2/20180321047.png)

`대상 그룹` 확인

![048](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/e47184f9a35801e607317fed8c5601f5966cfdf2/20180321048.png)

ALB의 DNS 접속확인

![049](https://gist.githubusercontent.com/yeongjun-yu/d41f2ac53b4d7681f89317201c5ba8dd/raw/e47184f9a35801e607317fed8c5601f5966cfdf2/20180321049.png)

End.

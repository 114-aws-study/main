일일사 AWS스터디 CodeDeploy핸즈온(2018-05-12)
======

일일사 AWS스터디 핸즈온(2018-05-12) 내용을 복습하며 스크린캡쳐 한 자료임.

## CodeDeploy EC2 정책(Policy)작성

![001](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/001.png)


```json
{
   "Version": "2012-10-17",
   "Statement": [
       {
           "Effect": "Allow",
           "Action": [
               "s3:Get*",
               "s3:List*"
           ],
           "Resource": "*"
       }
   ]
}
```

![002](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/002.png)

![003](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/003.png)

## 작성 확인
![004](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/004.png)

![005](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/005.png)

## CodeDeploy EC2역할(Role)에 정책추가

![006](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/006.png)

![007](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/007.png)

![008](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/008.png)

![009](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/009.png)

## CodeDeploy서비스 역할(Role)추가

![010](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/010.png)

![011](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/011.png)

![012](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/012.png)

![013](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/013.png)

## 신뢰관계 수정

![014](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/014.png)

![015](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/015.png)

```
"Service": "codedeploy.ap-northeast-1.amazonaws.com"
```

![016](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/016.png)

## 변경확인
![017](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/017.png)

## 로드밸런서 추가
![018](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/018.png)

![019](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/019.png)

![021](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/021.png)

![022](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/022.png)

![023](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/023.png)

![024](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/024.png)

![025](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/025.png)

![026](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/026.png)

![027](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/027.png)

![028](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/028.png)

![029](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/029.png)

## 오토스케일링 그룹 추가

![031](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/031.png)

![032](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/032.png)

![033](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/033.png)


```bash
#!/bin/bash
yum -y update
yum install -y aws-cli httpd
echo "<br>Hello" > /var/www/html/index.html
chkconfig httpd on
service httpd start
cd /home/ec2-user
aws s3 cp s3://aws-codedeploy-ap-northeast-1/latest/install . --region ap-northeast-1
chmod +x ./install
./install auto
```

![034](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/034.png)

![035](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/035.png)

![036](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/036.png)

![037](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/037.png)

![038](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/038.png)

![039](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/039.png)

![041](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/041.png)

![042](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/042.png)

![043](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/043.png)

![044](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/044.png)

![045](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/045.png)

![046](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/046.png)

![047](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/047.png)

![048](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/048.png)

![049](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/049.png)

## S3업로드

[deploy001.tar.gz]('./deploy001.tar.gz')

![051](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/051.png)


![052](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/052.png)

![053](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/053.png)

![054](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/054.png)

![055](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/055.png)

![056](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/056.png)

![057](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/057.png)

![058](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/058.png)

![059](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/059.png)

![061](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/061.png)

![062](https://gist.githubusercontent.com/yeongjun-yu/8cfbd21862f213bcdf999e837098ebb5/raw/c51c162dd32ec7b36dd4cddfcfd7faecccda548d/062.png)

END

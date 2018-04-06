일일사 AWS스터디 핸즈온 숙제 2018-03-21
======

## 로드 밸런서(ALB)
![001](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402001.png)
![002](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402002.png)
![003](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402003.png)
![004](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402004.png)
![005](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402005.png)
![006](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402006.png)
![007](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402007.png)
![008](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402008.png)
![009](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402009.png)

## 확인
![010](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402010.png)
![011](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402011.png)

## Auto Scaling
![012](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402012.png)
![013](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402013.png)
![014](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402014.png)
![015](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402015.png)
![016](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402016.png)

유저 데이터 예
```
#!/bin/bash
yum update -y
yum install -y gcc make nginx mysql56
chkconfig --level 345 nginx on
service nginx start
wget -O /tmp/stress-ng-0.09.04.tar.gz http://kernel.ubuntu.com/~cking/tarballs/stress-ng/stress-ng-0.09.04.tar.gz
tar zxvf /tmp/stress-ng-0.09.04.tar.gz -C /tmp
cd /tmp/stress-ng-0.09.04
make
mv stress-ng /usr/local/bin
```

![017](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402017.png)
![018](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402018.png)
![019](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402019.png)
![020](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402020.png)
![021](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402021.png)
![022](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402022.png)
![023](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402023.png)
![024](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402024.png)
![025](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402025.png)
![026](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402026.png)
![027](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402027.png)
![028](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402028.png)
![029](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402029.png)
![030](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402030.png)
![031](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402031.png)
![032](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402032.png)
![033](https://gist.githubusercontent.com/yeongjun-yu/658c9ea9e68e77ceeddcffc2ca27af37/raw/b8d6151ed83b0ed82ff99442ba754de20e8a3669/20180402033.png)

End.

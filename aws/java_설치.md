# ec2에서 java 설치

-----

### 1. open JDK 다운로드 사이트
> https://jdk.java.net/archive/

### 2. wget (다운로드)
> wget [Download URL]

### 3. 환경변수 설정

1. vi /etc/profile 편집

```
설치한 java 위치 지정
export JAVA_HOME=/usr/lib/jdk-17
```
2. source /etc/profile 명령어 실행
3. echo $JAVA_HOME 명령어 실행 (확인)
4. java -version 명령어 실행 (확인)
5. vi /etc/bashrc 편집 (별칭 지정)
```
alias java="/usr/lib/jdk-17/bin/java"
alias javac="/usr/lib/jdk-17/bin/javac"
```
7. source /etc/bashrc 명령어 실행
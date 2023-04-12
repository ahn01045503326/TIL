# Maven 기반 프로젝트에서 로컬 jar 라이브러리 추가

-----

### 1. pom.xml 수정
- Spring Boot는 빌드시 spring-boot-maven-plugin 플러그인을 사용한다. 
- 플러그인의 includeSystemScope 옵션을 true로 활성화해야 로컬 .JAR 파일을 프로젝트에 추가할 수 있다.
````
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <configuration>
        <includeSystemScope>true</includeSystemScope>
    </configuration>
</plugin>
````

- spring Framework는 아래 설정만 진행.
- .jar 파일을 추가 & 반드시 scope 옵션은 system으로 설정
````
<dependency>
    <groupId>org.jobrunr</groupId>
    <artifactId>jobrunr</artifactId>
    <version>4.0.4</version>
    <scope>system</scope>
    <systemPath>${pom.basedir}/src/main/resources/libs/jobrunr-4.0.4-bug-fixed.jar</systemPath>
</dependency>
````


---

### 2. local repository 설정
> 인텔리제이에서 설정하면 오류가 났다. 왜 그런지 이유는 모르겠다.
> 해당 설정을하면 .m2/repository 파일에서 가져오도록 설정.
> 해당 .jar 파일이 repository 디렉토리에서 못가져오는듯..

- local jar 파일을 프로젝트 디렉터리 내 규칙에 맞추어 넣는다.
- jar 파일을 넣는 규칙은 다음과 같다.
````
- 폴더 1
  - 폴더 2
    - ...
      - 파일명
        - 버전명
          - 파일명-버전명.jar
````

- pom.xml파일 내 local repository를 추가한다.
````
<repositories>
	<repository>
		<id>local-repository</id>
		<name>local repository</name>
		<url>file://${project.basedir}/[jar가 위치한 경로]</url>
	</repository>
</repositories>
````

- pom.xml파일 내 dependency를 추가한다.
````
<dependencies>
	<dependency>
		<groupId>[폴더 1].[폴더 2].[...]</groupId>
		<artifactId>[파일명]</artifactId>
		<version>[버전명]</version>
	</dependency>
</dependencies>
````

- -U옵션을 사용해 maven을 패키징 한다.
````
mvnw clean package -U
````

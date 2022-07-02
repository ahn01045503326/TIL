# mysqldump

-----

### 모든 데이터베이스 백업
> mysqldump -uroot -p[비밀번호] --all-database > 파일명

### 특정 DB 백업
> mysqldump -uroot -p[비밀번호] DB이름 > 파일명

### 특정 DB의 특정 테이블만 백업
> mysqldump -uroot -p[비밀번호] --no-create-info [DB이름] [테이블명] > 파일명
# SQL Server

SQL Server의 데이터베이스는 구조화된 데이터의 특정 집합이 저장되는 테이블 모음으로 구성     
행 : record, tuple
열 : attribute

--------------
## 데이터 베이스의 기본 정보

SQL Server의 인스턴스가 하나 이상 설치될 수 있음     
각 인스턴스는 하나 이상의 데이터베이스를 포함할 수 있음     
데이터베이스 내에 스키마가 하나 이상 포함될 수 있음      
각 스키마에는 테이블, 뷰, 저장 프로시저와 같은 데이터베이스 개체가 존재    

SQL Server 데이터베이스는 파일 시스템에 파일로 저장됨   

--------------
## 데이터베이스 만들기

### 제한사항

하나의 인스턴스 당 최대 32,767개의 데이터 베이스를 지정할 수 있음    

### 필수조건   

CREATE DATABASE 문은 기본 트랜잭션 관리 모드(autocommit moded)에서 실행해야함   
명시적/암시적 트랜잭션에서 허용되지 않음   

### 권한

master 데이터베이스의 CREATE DATABASE 권한이 있거나 CREATE ANY DATABASE 또는 ALTER ANY DATABASE 권한이 있어야 함   
인스턴스의 디스크 사용 제어를 위해 일반적으로 생성 권한은 일부 로그인 계정으로 제한됨

### Transact-SQL 사용

1. 데이터 베이스 엔진에 연결
2. 표준 도구 모음에서 새 쿼리 선택
3. 다음 쿼리를 사용하여 실행

```
USE master ;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```
keyword PRIMARY가 사용되지 않았기 때문에 첫번째 파일인 Sales_dat이 주 파일이 됨   
'SIZE'에서 MB인지 KB인지 명시되지 않았기 때문에 MB로 할당됨   
Sales_log에서 'SIZE'가 MB로 할당되었기 때문에 MB로 할당됨   

----------------



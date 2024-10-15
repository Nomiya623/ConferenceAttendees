# 📦 ASP.NET Core API와 SQL Server Docker 컨테이너화 프로젝트

이 프로젝트는 **ASP.NET Core API**와 **SQL Server 데이터베이스**를 Docker로 컨테이너화하여 일관된 배포 및 확장 가능한 클라우드 애플리케이션을 구축

## 🚀 프로젝트 개요
- **SQL Server 컨테이너 설정**: SQL Server를 Docker 컨테이너에서 설정.
- **ASP.NET Core API 컨테이너화**: ASP.NET Core API를 Docker로 컨테이너화하여 배포를 지원.
- **EF Core를 통한 데이터베이스 마이그레이션 및 시딩**: Docker 환경에서 Entity Framework Core를 사용하여 데이터베이스를 마이그레이션.
- **컨테이너화된 API와 데이터베이스 연결**: 컨테이너화된 API를 컨테이너화된 데이터베이스와 연결하는 모범 사례.
- **Docker 내부 네트워크 사용**: Docker의 내부 네트워크를 사용하여 컨테이너 간의 원활한 통신 설정.

---

## 🛠 Docker 설정

### 1️⃣ SQL Server 컨테이너 실행

```bash
docker pull mcr.microsoft.com/mssql/server
docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=Str0ngPa$$w0rd' -p 1400:1433 -d mcr.microsoft.com/mssql/server

```
### 2️⃣ ASP.NET Core API 컨테이너 빌드 및 실행

프로젝트 디렉토리로 이동하여 Docker 이미지를 빌드하고 컨테이너를 실행:
```bash
# 프로젝트 디렉토리로 이동
cd C:\Users\infinitt\source\repos\ConferenceAttendees.CloudNativeDevelopment-master

# Docker 이미지를 빌드
docker build -t conferenceattendeesapi:latest .

# Docker 컨테이너 실행
docker run -d -p 8081:80 conferenceattendeesapi:latest
'''
```
위 명령어는 conferenceattendeesapi라는 이름으로 Docker 이미지를 빌드하고, API를 포트 8081에서 컨테이너 실행.

## 🔗 API와 데이터베이스 연결
Docker 내부 네트워크를 사용하여 컨테이너 간 통신을 설정. localhost 대신 host.docker.internal을 사용하여 API에서 데이터베이스에 연결.

appsettings.Development.json 파일에서 연결 문자열을 다음과 같이 설정합니다:
```bash
"ConnectionStrings": {
  "ConferenceAttendeeDatabaseConnection": "Server=host.docker.internal,1400;Database=ConferenceAttendeeDb;Trusted_Connection=false;MultipleActiveResultSets=true;Encrypt=false;user id=sa;password=Str0ngPa$$w0rd;"
}
```
appsettings.json (Docker)
```bash
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=friendly_turing,1433;Database=ConferenceAttendeeDb;User Id=sa;Password=Str0ngPa$$w0rd;"
  },
```

### 📂 EF Core 데이터베이스 마이그레이션
데이터베이스 마이그레이션을 적용하여 스키마를 최신 상태로 유지합니다. Visual Studio의 NuGet 패키지 관리자 또는 .NET CLI를 사용하여 마이그레이션을 추가하고 데이터베이스를 업데이트 필요.

Visual Studio에서 패키지 매니저 콘솔에서 명령:
```bash
# 마이그레이션 추가
add-migration InitialMigration

# 마이그레이션 적용
update-database
```
또는 .NET CLI를 사용할 경우:
```bash
# 마이그레이션 추가
dotnet ef migrations add InitialMigration

# 마이그레이션 적용
dotnet ef database update
```
이 단계는 데이터베이스 스키마를 최신 상태로 유지하며, 마이그레이션을 통해 자동으로 데이터베이스를 설정.


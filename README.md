# 📦 ASP.NET Core API와 SQL Server Docker 컨테이너화 프로젝트

이 프로젝트는 **ASP.NET Core API**와 **SQL Server 데이터베이스**를 Docker로 컨테이너화하여 일관된 배포 및 확장 가능한 클라우드 네이티브 애플리케이션을 구축

## 🚀 프로젝트 개요
- **SQL Server 컨테이너 설정**: SQL Server를 Docker 컨테이너에서 빠르고 효율적으로 설정.
- **ASP.NET Core API 컨테이너화**: ASP.NET Core API를 Docker로 컨테이너화하여 일관성 있는 배포를 지원.
- **EF Core를 통한 데이터베이스 마이그레이션 및 시딩**: Docker 환경에서 Entity Framework Core를 사용하여 데이터베이스를 마이그레이션하고 시드하는 방법.
- **컨테이너화된 API와 데이터베이스 연결**: 컨테이너화된 API를 컨테이너화된 데이터베이스와 연결하는 모범 사례.
- **Docker 내부 네트워크 사용**: Docker의 내부 네트워크를 사용하여 컨테이너 간의 원활한 통신 설정.

---

## 🛠 Docker 설정

### 1️⃣ SQL Server 컨테이너 실행

```bash
docker pull mcr.microsoft.com/mssql/server
docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=Str0ngPa$$w0rd' -p 1400:1433 -d mcr.microsoft.com/mssql/server

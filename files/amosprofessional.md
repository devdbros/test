## Amos Professional 운영


#### 프로젝트 개요    
| 프로젝트명 | Amos Professional 운영 |
| ------ | ------ |
| 기획 | Unit K > 디지털마케팅본부 > 기획3그룹 > 기획3팀 > 최은정 과장, 김경자 대리 |
| 퍼블 | 퍼블리셔팀 > 황규정 과장, 이명민 주임 |
| 개발 | 개발팀 > 이슬기 대리 |
| 개발 URL | http://10.155.8.24:8329/kr/index.jsp |
| 서비스 URL | http://www.amosprofessional.com |
| SSL | https://www.amosprofessional.com |
| 어드민 URL | http://www.amosprofessional.com/as/index.jsp (계정:sglee / rhksflwk.1) |
| 상태 | 유지보수중 |
| 비고 | 개발, 관리자는 vpn 접속 후 접근 가능 (신규계정 관리자 접근 시 /as/index.jsp 상단에 VPN IP 추가) |


#### 웹서버 정보
|  |  |
| ------ | ------ |
| 서버 정보 | (개발)10.155.8.24 (운영)10.155.8.25, 26 |
| FTP | VDI 내 https://sac.amorepacific.com  (각 사용자 계정/암호) |
| ROOT PATH | /app/was8.0/WEB-B/yp_amos_kr_2013/yp_amos_kr_2013.ear/Amos_Web.war/ |
| 웹서버 | JSP 2.1 |
| Git | https://gitlab.dbroscreative.com/project.2017/amos-professional.git |
| 비고 | include 된 파일 수정 후 SAC > SSH 에서 touch |
1. VPN -> VDI(공통계정) -> SAC -> SFTP 접속(IAM에서 설정한 암호)


#### DB 정보 (개발)
|  |  |
| ------ | ------ |
| DB 종류 | Oracle 11g 11.2.0.4.0 |
| 서버정보 | 10.155.8.80:1521 |
| 디비계정 | DB명:UXUTF2, 계정: AMOSDBA, 암호: DBA#09AMOS |

#### DB 정보 (운영)
|  |  |
| ------ | ------ |
| DB 종류 | Oracle 11g 11.2.0.3.0 |
| 서버정보 | 10.129.28.121:1521 |
| 디비계정 | DB명:APWEBDB, 계정: AMOSDBA, 암호: DBA$09AMOS |
````
- 운영 DB는 Chakra 로그인 후 접근 가능.
````

#### 특이사항
1. VPN 신규 계정 생성 및 기타 문의
 - 이시형 <ajouface@amorepacific.com>     
2. Naver Map API ClientID : S98_Wos3hK8JWDQkaap3

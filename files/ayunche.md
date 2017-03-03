## 아윤채 운영


#### 프로젝트 개요
| 프로젝트명 | 아윤채 운영 |
| ------ | ------ |
| 기획 | Unit K > 디지털마케팅본부 > 기획3그룹 > 기획2팀 > 이승후 과장,  기획3팀 > 김경자 대리 |
| 퍼블 | 퍼블리셔팀 > 황규정 과장, 이명민 주임 |
| 개발 | 개발팀 > 이슬기 대리 |
| 개발 URL | http://10.155.8.24:8309/index.jsp |
| 서비스 URL | http://www.ayunche.com |
| SSL |  |
| 어드민 URL | http://www.ayunche.com/_admin/index.jsp  |
| 상태 | 유지보수중 |
| 비고 | 개발 URL ; vpn 접속 후 접근 가능  |


#### 웹서버 정보
|  |  |
| ------ | ------ |
| 서버 정보 | (개발) 10.155.8.24  (운영) 10.155.8.25, 10.155.8.26 |
| FTP | VDI 내 https://sac.amorepacific.com (각 사용자 계정/암호) |
| ROOT PATH | /app/was8.0/WEB-A/yp_ayunche_kr_2012/yp_ayunche_kr_2012.ear/yp_ayunche_kr_2012.war/ |
| 웹서버 | JSP 2.1 |
| Git | https://gitlab.dbroscreative.com/project.2017/ayunche.git |
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

# [IAM Workshop](https://catalog.us-east-1.prod.workshops.aws/workshops/dd23d392-bea4-483c-aefd-f62ed73f936d/en-US)
# 정책(Policy)
## 자격증명 기반 정책 (Identity-based policies)
### 1. AWS 관리형 정책 (AWS Managed policies)
  - AWS에서 제공하는 글로벌 적용 가능 정책
  - 정책 이름 앞에 주황색 정육각형의 AWS 아이콘이 표시되어져 있다.
### 2. 고객 관리형 정책 (Customer Managed policies)
  - 고객이 직접 생성한 정책
  - **고객 계정에서만 사용 가능한 정책**
### 3. 인라인 정책 (In-line policies)
  - 단일 사용자 그룹 역할에 직접 추가하는 정책
  - **재활용 불가**
## 권한 경계 정책 (Permissions boundaries)
- IAM 엔터티에 부여할 수 있는 최대 권한을 설정하는 고급 기능
- 자격증명 기반 정책과 같이 사용하여 IAM 엔터티의 **허용범위를 제약하는 방법으로 효과적**
- IAM 엔터티는 자격증명 기반 정책과 권한 경계 정책 모두에서 허용되는 작업만 수행할 수 있다.(교집합)
## 리소스 기반 정책 (Resource-based policies)
- 해당 리소스에서 특정 작업을 수행할 수 있는 권한을 지정된 보안 주체에게 부여하고 이러한 권한이 적용되는 조건을 정의한다.
- 리소스 기반 정책은 인라인 정책

# 역할(Role)
## RBAC(Role-Based Access Control)
- RBAC을 사용하게 되면 그룹 또는 사용자에게 직접 권한을 주지 않고, 여러 권한의 논리적인 집합들을 역할(Role)로 만들고 그룹 또는 사용자에게 연결 할 수 있습니다.
이렇게 되면 필요에 따라 역할을 부여할 수 있으므로 복잡하고, 경직되게 권한을 관리하지 않아도 됩니다.
- 그룹 또는 사용자에게 역할전환을 통해 새로운 권한 집합만을 사용할 수 있게 할 수 있다.

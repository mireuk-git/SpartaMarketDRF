# :guardsman: 우리를 위한 중고거래 :: SpartaMarket :carrot:
Sparta Ch4. Django project

---

## :guardsman:프로젝트 소개
우리를 위한 중고거래 :: SpartaMarket(이하 SpartaMarket)은 사용자가 온라인 상에서 쉽고 빠르게 중고물품 거래를 가능하게 하는 웹 서비스입니다. 

## :trophy:프로젝트 핵심 목표
DRF를 사용해 회원들이 쉽게 중고거래를 할 수 있게 하는 웹 애플리케이션의 웹 기능 구현
ERD를 작성하고 데이터베이스의 모델을 설계하는 연습

## :star2:주요 기능
- MVP(Minimum Viable Product):
  - 회원가입
    - Endpoint: `/api/accounts`
    - Method: `POST`
  - 로그인
    - Endpoint: `/api/accounts/login`
    - Method: `POST`
  - 프로필 조회
    - Endpoint: `/api/accounts/<str:username>`
    - Method: `GET`
- 상품 관련 기능
  - 상품 등록
    - Endpoint: `/api/products`
    - Method:`POST`
  - 상품 목록 조회
    - Endpoint: `api/products`
    - Method: `GET `
  - 상품 수정
    - Endpoint: `/api/products/<int:productId>`
    - Method: PUT
  - 상품 삭제
    - Endpoint: `/api/products/<int:productId>`
    - Method: `DELETE`

---

## :file_folder:Entity Relationship Diagram
![](spartamarket.png)

user - 계정 관련된 기능을 다루는 개체, 실제 이름은 accounts이다.
<details>
<summary>User 속성</summary>

- Username: 계정명
- password: 계정의 비밀번호
- My_item_ID: 자신이 등록한 게시물(물품)의 ID
- Want_item_ID: 자신이 찜한 게시물(물품)의 ID
- Follow: 자신이 팔로우한 계정의 username
- Follower_num: 자신이 팔로우한 계정의 수, 실제로 구현되진 않음
</details>

<br>
<br>

Item(products) - 상품 관련된 기능을 다루는 개체, 실제 이름은 articles로 되어있다. 
<details>
<summary>Item 속성 </summary>

- ItemID: 게시물의 식별용 ID, username과 달리 게시물은 제목으로 식별하지 않고 해당 속성으로 식별한다. 
- price: 물품의 가격, 실제로 구현이 되지 않았고 작성자가 직접 게시글의 내용에 가격을 적는 형태로 구현
- quantity: 물품의 갯수, 실제로 구현되지 않고 작성자가 직접 게시글의 내용에 가격을 적게 변경
</details>


### :open_file_folder:프로젝트에 포함된 App
#### Accounts
기본적인 회원 기능과 유저별 프로필 페이지 및 그와 관련된 기능들이 포함되어 있다. 

<details>
<summary> views </summary>

- signup - POST request를 받아 새 계정 생성
201: 정상적으로 새 계정 생성됨
400: 잘못된 요청
- login - POST request를 받아 로그인
200: 로그인 성공
400: 잘못된 요청, 이메일 또는 비밀번호가 올바르지 않음
- logout - POST request를 받아 로그아웃
400: 로그아웃 실패
- delete - POST request를 받아 계정을 auth_user에서 삭제
- profile 
  - GET: 프로필 페이지로 이동
    - 200: 성공적으로 프로필 페이지 데이터를 얻어옴
  - PUT,PATCH: 회원정보 수정
    - 200: 성공적으로 회원정보 수정
- follow: 팔로우 기능
  - 200: 성공적으로 팔로우/팔로우 해제
  - 400: 자기자신을 팔로우 할 경우의 오류 메시지

</details>

#### Articles
물건 목록 페이지와 개별 물건의 디테일 페이지, 그리고 그와 관련된 게시, 삭제, 수정 등의 기능이 포함되어 있다, 

<details>
<summary> views </summary>

- ArticleListCreate.get - 게시글 목록 조회 
- post - 게시글 생성
  - 201: 성공적으로 새 게시글 생성됨
  - 400: 새 게시글 생성 오류

- get_object - 게시글 반환, ArticleDetail.get의 부속품
  - 404: 게시글이 존재하지 않음
- ArticleDetail.get - 게시글 상세 조회, 조회수 계산

- CommentListCreate.get-article - 게시글 반환, CommentListCreate 클래스의 메서드의 부속품
  - 404: 게시글이 존재하지 않음
- CommentListCreate.get - 댓글 목록 조회
- CommentListCreate.post - 새 댓글 생성
  - 201: 댓글 성공적으로 생성
  - 400: 댓글 생성 실패

- CommentLike.get_article - 게시글 반환, CommentLike.post의 부속품
- CommentLike.get_comment - 댓글 반환, CommentLike.post의 부속품품
- CommentLike.post - 댓글의 좋아요 토글 기능
  - 200: 성공적으로 처리 완료

</details>

## :mag_right:성과 및 회고
DRF를 이용해 데이터베이스 모델을 설계 및 구현해보는데 의의를 두었다. 해당 프로젝트를 진행하면서 DRF를 이용해 웹 서비스를 개발하는 과정과 연관된 경험을 쌓을 수 있었다. 
향후 비밀번호 변경 기능, 회원 탈퇴 기능, 페이지네이션 및 필터링, 카테고리 기능, 게시글 좋아요 기능, 태그 기능 등을 추가할 계획이 있다. 또한 아직 프론트엔드가 구현되지 않았기에 프론트엔드 구현 또한 프로젝트 발전을 위한 선택지 중 하나가 되겠다. 
# 개발하기 전 준비

## 용어

제시된 용어

- Product: 상품
    - Summary: 상품에 대한 요약 정보
    - Detail: 상품에 대한 상세 정보
    - Image: 상품 이미지
    - Option: 상품에 대한 상세 옵션 종류 (색상, 크기 등)
        - OptionItem: 옵션에 대한 상세 옵션 값 (옵션이 색상이라면 이건 Blue, Red 같은 걸 의미함)
- Category: 상품에 대한 분류
- Cart: 장바구니
    - LineItem: 장바구니에 담긴 것 (상품, 옵션, 수량 등을 동시에 다룸)
        - 여기서도 Option과 OptionItem을 사용한다.
        - 용어는 동일하지만 Product와 다른 구성을 갖기 때문에, 여기서는 Product와 Order라는 접두어를 활용한다.
        - 시스템을 분리할 수 있다면, 근본적으로 나누는 걸 추천(상품 정보 확인 / 장바구니 / 주문).
- Order: 주문
    - 여기서도 동일한 LineItem 활용.
- User: 사용자

## 과정

1. 용어 정의
2. 기능 정의
3. 화면url 정의
4. REST API spec 정의
5. 개발 환경 세팅
  - routing
  - CSS in JS
  - 의존성 주입
  - External store
  - test(jest, MSW, CodeceptJS(E2E))
  - backend
---
layout: post
title: HAL/HATEOAS
tags:
- hal
- hateoas
- tags
---

![](../img/interface.png)

## 개요

- Hypertext Application Language (HAL)
- JSON 또는 XML 코드 내의 외부 리소스에 대한 링크와 같은 하이퍼 미디어를 정의하기위한 2012년 6월에 처음 제안된 인터넷 초안 `표준` 규칙
- media type : application/hal+xml 및 media type : application/hal+json

## 협약

- 리소스와 링크의 두 가지 개념을 기반으로 요소를 표현하는 방식으로 구성

| 리소스 | 링크 |
| ------ | ------ |
| URI 링크, 내장 리소스, 표준 데이터 (JSON 또는 XML) 및 비 URI 링크로 구성 | 링크 이름 (‘rel’이라고도 함)뿐만 아니라 비추천 및 내용 협상에주의하도록 설계된 선택적 속성 |

## HATEOAS?? HAL??

- HATEOAS(Hypermedia As The Engine Of Application State) 는 `REST 어플리케이션 아키텍처`의 구성요소
- 즉 `HAL 표준을 사용`하는 특정 `인터페이스`라고 볼 수 있음
- Spring Framework 에서 HATEOAS 라이브러리(=Spring HATEOAS) 를 제공해 주어 보다 편리하게 사용 가능함

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-hateoas</artifactId>
</dependency>
```

## 예시

- 요청 URL

```
GET /product/1
```

- 기존 방식

```json
{
  "productId": 1,
  "name": "ABC",
  "description": "Product ABC",
  "unitPrice": 9.99
}
```

```xml
<Product>
    <ProductId>1</ProductId>
    <Name>ABC</Name>
    <Description>Product ABC</Description>
    <UnitPrice>9.99</UnitPrice>
</Product>
```

- HATEOAS
  - links : 더 자세한 정보를 제공함
  - 나머지는 일반 리턴값과 동일
```json
{
  "_links": {
    "self": {
      "href": "/product/1"
    },
    "collection": {
      "href": "/products"
    },
    "templated": {
      "href": "/product/{productId}",
      "templated": true
    }
  },
  "productId": 1,
  "name": "ABC",
  "description": "Product ABC"
  "unitPrice": 9.99
}
```

```json
{
  "_links": {
    "deposit": "/accounts/1/deposit",
    "withdraw": "/accounts/1/withdraw",
    "transfer": "/accounts/1/transfer",
    "close":"/accounts/1/close"
  },
  "account_number":1,
  "balance":{
    "currency":"usd",
    "value":100.00
  }
}
```


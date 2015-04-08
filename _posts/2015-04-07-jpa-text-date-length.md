---
title: JPA에서 Text 데이터를 저장하는 방법
layout: post
categories:
  - Java
  - Mysql
  - JPA
tags:
  - JPA
  - mysql
  - annotation
  - text
---

`JPA` 어노테이션을 이용해 TEXT 데이터 타입을 사용하는 경우 여러가지 방법이 있다.
`@Lob`을 사용하는 방법도 있고 `columndefinition`을 `TEXT`로 주는 방법도 있다.
정답이 있다기보다는 용도와 데이터의 용량에 따라 적절한 선택을 하는 것이 필요하다.


* VARCHAR: 65,535 bytes (~64Kb, 21,844 UTF-8 encoded characters)

* TEXT: 65,535 bytes (~64Kb, 21,844 UTF-8 encoded characters)

* MEDIUMTEXT: 16,777,215 bytes (~16Mb, ~5.5 million UTF-8 encoded characters)

* LONGTEXT: 4,294,967,295 bytes (~4GB, ~1.4 billion UTF-8 encoded characters).
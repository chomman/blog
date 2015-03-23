---
title: JPA CascadeType 종류
layout: post
categories:
  - Java
  - JPA
  - Programming
tags:
  - cascade
  - CascadeType
  - detached entity passed to persist
  - jpa
  - PersistentObjectException
---
개발도중 PersistentObjectException: detached entity passed to persist 라는 에러메세지를 만나게 되었다.

JPA 사용시 자동으로 생성되는 값을 가진 필드에 직접 값을 할당해 저장하고자 할 때 발생되는 에러다.

Self Join 도메인에서 @ManyToOne 의 옵션으로 Cascade 를 CascadeType.All 로 지정했는데 이 때문이었다.

&nbsp;

CascadeType의 종류에는 다음과 같은 것들이 있다.

  * CascadeType.RESIST &#8211; 엔티티를 생성하고, 연관 엔티티를 추가하였을 때 persist() 를 수행하면 연관 엔티티도 함께 persist()가 수행된다.  만약 연관 엔티티가 DB에 등록된 키값을 가지고 있다면 detached entity passed to persist Exception이 발생한다.
  * CascadeType.MERGE &#8211; 트랜잭션이 종료되고 detach 상태에서 연관 엔티티를 추가하거나 변경된 이후에 부모 엔티티가 merge()를 수행하게 되면 변경사항이 적용된다.(연관 엔티티의 추가 및 수정 모두 반영됨)
  * CascadeType.REMOVE &#8211; 삭제 시 연관된 엔티티도 같이 삭제됨
  * CascadeType.DETACH &#8211; 부모 엔티티가 detach()를 수행하게 되면, 연관된 엔티티도 detach() 상태가 되어 변경사항이 반영되지 않는다.
  * CascadeType.ALL &#8211; 모든 Cascade 적용

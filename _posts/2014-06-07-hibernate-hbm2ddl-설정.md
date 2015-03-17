---
title: Hibernate hbm2ddl 설정
layout: post
categories:
  - Java
tags:
  - hbm2ddl
  - hibernate
  - java
  - 하이버네이트
---
Hibernate 설정정보 중에는 hbm2ddl 이라고 하는 놈이 있습니다.

이는 하이버네이트의 매핑 설정 정보를 가지고 DB 스키마의 CREATE, UPDATE, VALIDATE 기능을 정의하는 기능입니다.

hibernate.hbm2ddl.auto 의 설정 옵션은 다음과 같습니다.

  * create : 무조건 테이블 생성, classpath에 import.sql이 있을 때 import.sql 파일의 sql문을 수행한다.
  * create-drop : create 기능과 동일하나 기존에 동일한 테이블이 존재하는 경우 drop을 우선 수행한다.
  * update : 테이블이 없을 경우 테이블을 생성하고, 있을 경우 테이블의 컬럼 구조를 변경
  * validation : 테이블 스키마의 유효성을 확인하기만 한다.

&nbsp;

실제 설정은 이렇게 합니다.

<bean id="hibernateProperties" class="org.springframework.beans.factory.config.PropertiesFactoryBean">
    <property name="properties">
		<prop key="hibernate.dialect">org.hibernate.dialect.MySQLDialect</prop>
		<prop key="hibernate.show_sql">true</prop>
		<prop key="hibernate.hbm2ddl.auto">update</prop>
		<prop key="jdbc.fetch_size">50</prop>
		<prop key="jdbc.batch_size">25</prop>
		<prop key="hibernate.cache.use_query_cache">true</prop>
		<prop key="hibernate.cache.provider_class">org.hibernate.cache.EhCacheProvider</prop>
		<prop key="hibernate.query.substitutions">true 1,false 0</prop>
    </property>
</bean>
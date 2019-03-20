---
layout: post
title: Spring 01 Infrastructure
categories: Spring
description: Spring 01 Infrastructure
keywords: Java, Spring
---

# Infrastructure

## BeanDefinition
> A BeanDefinition describes a bean instance, which has property values,
> constructor argument values, and further information supplied by
> concrete implementations.

## BeanFactory
> Used to dereference a FactoryBean instance and distinguish it from
> beans created by the FactoryBean.

## ApplicationContext
> Central interface to provide configuration for an application.
> This is read-only while the application is running, but may be
> reloaded if the implementation supports this.

## BeanFactoryPostProcessor
> Allows for custom modification of an application context's bean definitions,
> adapting the bean property values of the context's underlying bean factory.

We can modify the bean definition registered in the context before initialization.

## BeanPostProcessor
> Factory hook that allows for custom modification of new bean instances,
> e.g. checking for marker interfaces or wrapping them with proxies.

Implementation of Spring AOP used it.


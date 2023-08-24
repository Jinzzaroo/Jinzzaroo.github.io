---
title: "[몰입교육] 쿠버네티스"
date: 2023-08-23T09:11:21+09:00
author : "Jinzzaroo"
draft: false
categories : ["몰입교육"]
tags : ["CI/CD", "쿠버네티스"]
---

Kubernates
===================

## Kubernates란?
쿠버네티스(k8s, Kubernates, 큐브)는 컨테이너화된 애플리케이션을 배포, 관리, 확장할 때 수반되는 다수의 수동 프로세스를 자동화하는 오픈소스 컨테이너 오케스트레이션 플랫폼

## Kubernates가 유용하게 된 배경
> 전통적 배포 시대 -> 가상화된 배포 시대 -> **컨테이너 배포 시대**

- 컨테이너는 앱을 포장하고 실행하는 좋은 방법이다.
- 원활한 로드밸런싱 및 유연한 대처 가능

## Kubernetes 구성요소

![image](https://blog.kakaocdn.net/dn/I4xZg/btrwIiichSc/6jHWmTh5kXX0Gv0GQ58vB0/tfile.svg)

### **클러스터 > 노드 > 파드 > 컨테이너**
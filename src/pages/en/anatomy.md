---
title: Anatomy of Kubeshark
description: Anatomy of Kubeshark
layout: ../../layouts/MainLayout.astro
mascot: Bookworm
---

Kubeshark consists of three separate programs; **CLI**, **Hub** and **Worker**.

## CLI

It's a binary distribution of the client that communicates with your cluster through K8s API.
Which you're going to use it to deploy the **hub**. This is the program which you need to [install](/en/install)
into your local machine.

## Hub

It's a Docker image which is deployed into your cluster as a normal pod. It orchestrates the **worker** deployments,
receives sniffed and dissected directed from each **worker** and collects into a central place.
It also serves a web interface to display the collected traffic on your web browser.

## Worker

It's a Docker image which is deployed into your cluster as a DaemonSet to ensure each node in your cluster
are covered by Kubeshark. The worker contains the implementations of network sniffer, kernel tracing and more.
Workers transmit the collected traffic to **hub**.

The worker by itself can be used as a network sniffer on your local machine.
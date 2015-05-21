---
layout: post
title: Monitoring MS SQL Cluster on windows with Zabbix 
---

> The goal is to monitor an active/passive cluster of MS SQL server in Zabbix
> We will try to use a minimalist approach.

## 1. Install Zabbix on all nodes
Configure each zabbix agent as active and passive

## 2. Declare each hosts and add a windows template on them
This will enable basic monitoring on each hosts. Use an active Windows template, so that the agent will send its data to Zabbix.

## 3. Create another host for the cluster
Use a passive MS SQL Template, and declare the VIP/Cluster DNS, so that Zabbix will go fetch its information directly on the active node.

This way, each node is monitored, and the active node has MS SQL Monitoring enabled.

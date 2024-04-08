---
weight: 999
title: "Pfsense Haproxy"
description: ""
icon: "article"
date: "2024-03-31T00:11:55+01:00"
lastmod: "2024-03-31T00:11:55+01:00"
draft: false
toc: true
---

# Setup pfsense

## Install via iso

In a VM with a static ip

## Configure pfsense


# Setup acme

## Create Account keys

1. Create an account key (auto generate everything)
2. create a new wildcard certificate. Select cloudflare as DNS and enter all API keys and tokens. You can find API Tokens and ID under Profile > API and Account and zone id on the right sidebar of the selected domain.
3. Renew certificate

# Setup haproxy

## Define backend

Just add a new backend with ip and port. 

## Define frontend

1. Add a new frontend

---
title: tampermonkey auto refresh script
date: 2022-05-07T12:49:50+08:00
draft: true
---

```javascript
// ==UserScript==
// @name         DiaoTao Auto Refresh
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  auto refresh diantao task page.
// @author       Sumwai
// @match        https://market.m.taobao.com/*
// @icon         https://www.google.com/s2/favicons?sz=64&domain=tampermonkey.net
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    setTimeout(() => {
      // 20 sec to reload
      console.log("refresh ... ");
      window.location.reload()
    }, 20000)
    // Your code here...
})();

```

---
title: "Tech Stack Foundations: UXP for Adobe Media Encoder"
description: "The web technologies and the UXP runtime behind Media Encoder plugins: HTML, CSS, JavaScript, the shared engine, and how panels and scripts use them."
keywords:
  - UXP
  - Adobe Media Encoder
  - tech stack
  - JavaScript
  - HTML
  - CSS
  - Spectrum
  - runtime
contributors:
  - https://github.com/karan0207
---

# Tech Stack Foundations

A UXP plugin is built from the web technologies you already know, running on a single runtime that Adobe ships inside Media Encoder and other applications.

## What you write in

* **HTML** defines your panel's structure.
* **CSS** styles it. Adobe's Spectrum design system gives you components that match the host UI.
* **JavaScript** holds your logic and calls the Media Encoder APIs.

You do not ship a browser. UXP provides a modern JavaScript engine and a curated set of web APIs, so behavior is consistent across the Adobe apps that support UXP.

## The two surfaces

UXP work in Media Encoder falls into two surfaces that share the same runtime:

* **Panels** render UI inside Media Encoder. A panel is the visible, interactive part of a plugin.
* **Scripts** run logic against the host, with or without UI, to inspect and drive the encoding queue.

Because both use one engine, the code, libraries, and patterns you learn carry across panels, automation, and other UXP-enabled Adobe applications.

## What is and is not available

UXP supports a focused subset of web platform features rather than everything a browser offers. When in doubt, check the [UXP API reference](../../../uxp-api/index.md) for the exact elements, styles, and modules that are supported, instead of assuming a browser API exists.

## Next

<DiscoverBlock slots="link, text"/>

[Nomenclature](../nomenclature/index.md)

Learn the terms these docs use and how they map to CEP and ExtendScript.

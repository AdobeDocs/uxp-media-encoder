---
title: UXP AME
description: "Build UXP plugins for Adobe Media Encoder: create panels, drive the render queue, and automate batch encoding with HTML, CSS, and JavaScript."
contributors:
  - https://github.com/karan0207
---

<Superhero variant="halfWidth" textColor="white" slots="heading, text, image" background="linear-gradient(135deg, #073B3A 0%, #0E6B61 100%)"/>

# Automate Adobe Media Encoder with UXP

Build plugins that run inside Media Encoder, discover presets, and drive the encoding queue. Turn repetitive exports into one-click workflows with HTML, CSS, and JavaScript.

![Build UXP plugins and automation for Adobe Media Encoder](images/hero.svg)

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. APIs and supported capabilities may change before general availability. Double-click installation is not available at launch and is expected to follow a few days later as part of the September Creative Cloud Desktop release.

<Resources slots="heading, links"/>

#### Resources

- [Get Started](get-started/index.md)
- [Set Up Media Encoder](get-started/developer-tools/index.md)
- [Render Queue Panel example](get-started/samples/render-queue-panel/index.md)
- [Media Encoder API reference](media-encoder-api/index.md)

## Choose Where to Start

A UXP plugin has two layers. The UXP runtime provides shared platform APIs for file access, storage, and networking. The Media Encoder API (the host DOM) drives the render queue, jobs, presets, and progress. Start with the path that matches what you need.

<Cards slots="image, heading, text, links" repeat="2" width="100%" />

![Learn the shared UXP platform](images/uxp-tutorials.svg)

### Learn the UXP platform

Walk through the full developer journey: build your first plugin, learn the platform and UXP APIs, and publish plugins.

[Start in the UXP Hub](https://developer.adobe.com/uxp/?aio_external)

![Build plugins for Adobe Media Encoder](images/media-encoder.svg)

### Use the Media Encoder API

Explore the Media Encoder DOM APIs and build your own plugin.

[Get Started](get-started/index.md)

**Note:** Start with the [UXP Hub](https://developer.adobe.com/uxp/?aio_external) to learn the fundamentals, core concepts, and the plugin development model. Use this Adobe Media Encoder UXP documentation for AME APIs, examples, and workflows. We will keep expanding these resources with more documentation and sample code throughout the beta.

## Explore APIs

Plugins use both layers: the Media Encoder API for encoding features, and the shared UXP APIs for platform capabilities like file access, storage, and networking.

<DiscoverBlock slots="link, text"/>

[Media Encoder API Reference](media-encoder-api/index.md)

The render queue, presets, jobs, progress reporting, watch folders, and other Media Encoder automation surfaces.

<DiscoverBlock slots="link, text"/>

[UXP API Reference](https://developer.adobe.com/uxp/uxp-api/?aio_external)

File system, networking, storage, HTML, CSS, and Spectrum UI capabilities shared by every UXP host.

## Join the Community

Join the worldwide community of Creative Cloud Developers building plugins and integrations to empower creativity.

Have questions while developing, or want to share feedback on the UXP documentation, APIs, samples, or other developer resources?

[Join the conversation in the Creative Cloud Developer Forums](https://forums.creativeclouddeveloper.com/) to connect with other developers, share your experiences, ask questions, and get support from the community.

Want to stay up to date with the latest developer news?

- [Subscribe to the Adobe Creative Cloud Developer Newsletter](https://www.adobe.com/subscription/ccdevnewsletter.html).

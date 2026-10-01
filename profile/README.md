# Nextcloud Publish

This project adds a lightweight publishing workflow to the [Nextcloud Collectives app](https://github.com/nextcloud/collectives), enabling users to turn collaboratively managed cloud content from their Collective markdown wikis into static websites and publish them online with a few clicks.

Collectives already supports public sharing, but publicly shared content remains tied to the Nextcloud instance and comes with limitations regarding performance, security, metadata exposure, and styling.
This project provides a dedicated workflow for turning collaboratively managed content into lightweight, static websites that can be published independently.

The publishing process creates a clear separation between internal collaboration and public presentation. Content can be developed and reviewed within a Collective before being published as a static website with reduced metadata and greater control over its presentation and styling.

<br/>

### Technical description

The publish service which Nextcloud Collectives calls via REST starts building the static websites and places them where a webserver e.g. nginx can serve them. The publish service consists of two parts which interact via a message broker. It receives build jobs via Rest, validates them and then enqueues them in the message broker. The ssg-worker listens on the message queue and when a build arrives, downloads the resources from NC Collective and builds a static website using the ssg-library. After that it moves the previously built static website to a specified webserver and notifies Nextcloud Collectives about success/failure.

The publish service can be deployed with a docker compose file offering an easy way via replica sets to spawn as much ssg-workers as needed to supply also lager setups with multiple Nextcloud instances using the same publish service. Isolating the build process into ssg-library with its templates makes building directly inside Nextcloud Collectives an option for small Nextcloud deployments.


<br/>

### Repositories

Since the project is  microservice architecture is going to be implemented as a microservice architecture, code can be found in multiple repositories:

[Nextcloud Collectives](https://github.com/nextcloud/collectives/pull/2769) – The Nextcloud collectives main repository with the UI part of the feature. The Pull Request for the project's feature can be found here: https://github.com/nextcloud/collectives/pull/2769

[SSG Library](https://github.com/nextcloud-publish/ssg-library) – The core library, that converts markdown delilvered by Collectives to a static site (HTML)

[Publish API](https://github.com/nextcloud-publish/publish) - Symfony php app providing a rest api receiving build jobs from NC collectives. Main repo of this project providing also docs and docker compose setup which can be used for deployment. [latest state](https://github.com/nextcloud-publish/publish/pull/35)

[SSG Worker](https://github.com/nextcloud-publish/ssg-worker) - Symfony php app building static websites using ssg-library. [latest state](https://github.com/nextcloud-publish/ssg-worker/pull/17)



<br/>
<br/>

### funded by
<a href="https://www.bmftr.bund.de/">
  <img width="300" alt="BMFTR Logo" src="https://github.com/user-attachments/assets/98751248-d8cc-405d-9b2d-bd031ac7047d" />
</a>

<br/>

<a href="https://www.prototypefund.de/">
  <img width="300" alt="Prototype Fund Logo" src="https://github.com/user-attachments/assets/ab533ff8-7cff-4428-b834-430857863acd" />
</a>

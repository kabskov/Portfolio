---
title: "Getting the deployment to work"
weight: 80
series: ["The Collector"]
series_order: 8
---
 
When I push code to `main`, a chain of tools takes over:
 
1. **GitHub Actions** builds the app and packs it into a Docker image (a package with everything the app needs to run).
2. The image is sent to **Docker Hub**.
3. **Watchtower** on my server (a DigitalOcean droplet) sees the new image and restarts the app with it.

In front of the app, **Caddy** handles HTTPS, and Postgres runs in its own container.
 
I followed the guide from our course materials, which made deploying pretty smooth. I did run into a few problems, but most of them were small:
 
- A missing slash in my JDBC URL made the app crash on startup.
- Caddy waits for the API to be healthy, but I had not made a healthcheck endpoint yet, so Caddy never started.
- Because of my context path, the healthcheck is at `/api/v1/auth/healthcheck`, not at the path in the guide.
- Docker Compose uses the **service name** (`collector`), for example in the Caddyfile and in `depends_on`. Docker commands and Watchtower use the **container name** (`the-collector`). I mixed these up at first, and that caused most of my trouble with container names.
- The Watchtower image in the guide is no longer maintained, so I switched to an active fork.

I skipped the last guide, about moving old projects, because I only needed my exam project running.
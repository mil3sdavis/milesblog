---
title: Building Single Sign-On for My Homelab with Authentik and Grafana
date: 2026-03-25
draft: false
tags:
  - blog
  - homelab
  - network
---
# Building Single Sign-On for My Homelab with Authentik and Grafana

## Introduction

Like many people running a homelab, I found myself with a growing collection of self-hosted services—Grafana for monitoring, Uptime Kuma for alerts, Portainer for container management, and more.

Each service worked well on its own, but there was one problem:  
**every service had its own login.**

It wasn’t just inconvenient—it also didn’t scale. Managing users, credentials, and access across multiple applications quickly becomes messy.

So I set out to solve a problem that’s very common in real-world environments:  
**centralized authentication with Single Sign-On (SSO).**

---

## The Goal

My objective was simple:

- One login for all services
    
- Centralized user management
    
- A system that mirrors enterprise identity platforms
    

In short, I wanted to turn my homelab into something that behaves more like a production environment.

---

## The Stack

To accomplish this, I used:

- **Authentik** – Identity provider (IdP) supporting OAuth2 / OpenID Connect
    
- **Grafana** – First application to integrate with SSO
    
- **Docker / Docker Compose** – Service deployment and orchestration
    
- **Uptime Kuma** – Monitoring and alerting
    

Grafana was the ideal starting point because it natively supports OpenID Connect (OIDC), making it a straightforward first integration.

---

## The Reality: It Wasn’t Smooth

Getting everything running wasn’t the hard part.  
Getting it to initialize _correctly_ was.

I ran into several issues along the way:

- Containers restarting due to missing environment variables
    
- Database migration failures
    
- Permission errors on mounted volumes
    
- Authentik starting in a partially initialized state
    
- A login page existing… but no admin user to log in with
    
- Redirect URI mismatches that silently broke authentication
    

At one point, I had a fully running Authentik instance—but no way to access the admin interface because the setup flow had failed earlier.

That was a turning point:  
I realized this wasn’t just about configuration—it was about understanding how these systems behave under the hood.

---

## The Breakthrough

The biggest improvement came from switching to the **official Authentik Docker Compose configuration**.

That resolved:

- Startup race conditions
    
- Migration inconsistencies
    
- Missing default flows
    

Once I let Authentik fully initialize without interruption, everything clicked into place. I was finally able to create an admin account and access the admin interface.

---

## Implementing SSO with Grafana

With Authentik working, I moved on to integrating Grafana.

The process looked like this:

1. Create an OAuth2 / OpenID Connect provider in Authentik
    
2. Register Grafana as an application
    
3. Configure redirect URIs
    
4. Add OIDC settings to the Grafana container
    

One of the most important lessons here was how strict OIDC is about redirect URIs.

Even small differences—like:

- `localhost` vs an IP address
    
- missing paths
    
- trailing slashes
    

…will break authentication.

Fixing this required aligning Grafana’s `root_url` with the exact redirect URI configured in Authentik.

---

## The Result

After everything was configured, the flow worked exactly as intended:

1. Navigate to Grafana
    
2. Click “Sign in with Authentik”
    
3. Get redirected to the Authentik login page
    
4. After authentication, return to Grafana automatically
    

If I was already logged into Authentik, the login step was skipped entirely.

That “instant login” moment is when it really clicked—  
**this is what real SSO feels like.**

---

## What I Learned

This project taught me far more than just how to configure a few containers.

Key takeaways:

- **Initialization order matters** in distributed systems
    
- **Authentication protocols (OIDC/OAuth2) are extremely strict**
    
- Small configuration mismatches can completely break auth flows
    
- Debugging containerized applications requires reading logs carefully and understanding dependencies
    
- Centralized identity is a force multiplier—it simplifies everything else
    

Most importantly, I learned how to troubleshoot a system that spans multiple services, each with its own state and behavior.

---

## What’s Next

With Grafana successfully integrated, the next steps are:

- Extending SSO to additional services
    
- Introducing a reverse proxy (Traefik) to protect apps without native OIDC support
    
- Moving from IP-based access to clean internal domains
    
- Adding HTTPS for secure internal access
    

---

## Final Thoughts

What started as a simple annoyance—too many logins—turned into a deep dive into identity systems, authentication flows, and containerized infrastructure.

This project pushed me beyond basic setup and into real-world problem solving.

And that’s exactly what makes a homelab valuable:  
**it’s a place to build, break, and truly understand how systems work.**
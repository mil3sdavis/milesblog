---
title: " Building a Real-Time Aircraft Tracker in My Homelab"
date: 2026-03-26
draft: false
tags:
  - blog
  - homelab
  - network
---


---

# ✈️ Building a Real-Time Aircraft Tracker in My Homelab

## Turning a Raspberry Pi and some containers into a live aviation dashboard

---

## 🧠 Introduction

One of the things I enjoy most about running a homelab is taking random pieces of technology and turning them into something genuinely useful (or at least really cool).

Recently, I set out to build a system that could answer a simple question:

```text
“What aircraft is closest to my house right now?”
```

That question turned into a full-blown project involving:

- a Raspberry Pi pulling real-time aircraft data
    
- a time-series database
    
- custom data transformations
    
- and a Grafana dashboard showing live results
    

Along the way, I also improved my overall homelab setup—working with Docker, reverse proxies, DNS, and system monitoring.

---

## 🏠 The Homelab Foundation

My setup is built around an older desktop that I repurposed as a home server. It’s not cutting-edge hardware, but it’s more than capable of running multiple services using Docker.

On top of that, I’ve layered a few core components:

- **Pi-hole** for network-wide ad blocking and DNS control
    
- **Nginx** as a reverse proxy for clean internal service URLs
    
- **Uptime Kuma** for monitoring and alerting
    
- **SSH with key-based authentication** for secure remote access
    

This gives me a flexible platform to spin up new services and experiment freely.

---

## 📡 Capturing Aircraft Data (ADS-B)

The heart of the project is a Raspberry Pi running ADS-B software.

Aircraft continuously broadcast telemetry such as:

- position (latitude/longitude)
    
- altitude
    
- speed
    
- identification codes
    

Using an antenna and ADS-B feeder software, I’m able to capture this data locally and expose it via:

```text
http://<pi-ip>:8080/data/aircraft.json
```

This endpoint returns a constantly updating JSON feed of nearby aircraft.

---

## 📈 Building the Data Pipeline

Once I had the data source, the next step was figuring out how to store and analyze it.

I ended up with this pipeline:

```text
ADS-B (Pi) → Telegraf → InfluxDB → Grafana
```

### InfluxDB

I used InfluxDB as a time-series database to store aircraft telemetry over time.

Getting this working involved:

- configuring organizations and buckets
    
- generating API tokens
    
- debugging authentication issues (plenty of 401 errors…)
    

### Telegraf

Telegraf pulls the JSON feed and writes structured data into InfluxDB.

This step was crucial for turning raw JSON into something queryable.

---

## 🧠 Making Sense of the Data (Flux)

Raw data isn’t very useful on its own. The real value came from writing **Flux queries** to transform it.

Some of the key things I implemented:

### ✈️ Aircraft Count

How many aircraft are nearby at any given moment.

### 🛫 Altitude Filtering

Filtering out high-altitude aircraft to focus on more interesting local traffic.

### 🔄 Deduplication

Each aircraft sends multiple messages, so I had to:

- group by aircraft (`hex`)
    
- select only the most recent data point
    

### 📍 Distance Calculation

This was the most interesting part.

Using my home’s latitude and longitude, I calculated an approximate distance to each aircraft and sorted them by proximity.

---

## 📊 Visualizing Everything with Grafana

With the data flowing and queries working, I built out dashboards in Grafana.

### Key Panels

#### ✈️ Aircraft Count

A simple stat panel showing how many planes are nearby.

#### 📈 Aircraft Over Time

A time-series graph showing traffic patterns.

#### 🛫 Low Flying Aircraft

A filtered view highlighting planes below a certain altitude.

#### 🔥 Closest Aircraft (My Favorite)

A stat panel that shows:

- the closest aircraft to my house
    
- its distance in miles
    
- its identifier (hex code for now)
    

Example:

```text
Aircraft: AC60EF  
Distance: 0.26 mi
```

---

## 🧹 Cleaning Up the Dashboard

A surprising amount of work went into making the dashboard readable:

- fixing messy field names (`_value`, etc.)
    
- removing duplicate rows
    
- reordering columns
    
- rounding values
    
- adding units and thresholds
    

Grafana is powerful, but getting clean visuals takes some effort.

---

## ⚠️ Challenges Along the Way

This project definitely wasn’t plug-and-play.

### 💻 Resource Limits

Running a full ROM library scan (RomM) at the same time as this project:

- maxed out CPU
    
- filled RAM
    
- triggered alerts
    

Lesson learned: **resource management matters**, especially on older hardware.

---

### 🔐 InfluxDB Authentication

I ran into multiple issues with:

- incorrect tokens
    
- mismatched organization names
    

Result: lots of `401 Unauthorized` errors until everything lined up exactly.

---

### 🧮 Flux Query Quirks

Flux is powerful—but also finicky.

I ran into:

- grouping issues
    
- time column problems
    
- math expression parsing errors
    

A lot of the work was figuring out how to structure queries correctly.

---

## 🚀 What I Built

At the end of all this, I now have:

```text
A self-hosted system that tracks aircraft in real time,
analyzes their proximity to my location,
and displays the results in a live dashboard.
```

It’s one of those projects that’s both:

- technically valuable
    
- and just plain fun to watch
    

---

## 🔮 What’s Next

There’s plenty of room to expand this:

- Replace hex codes with real **flight numbers / airline names**
    
- Add a **map visualization** of aircraft
    
- Trigger **alerts when planes get very close**
    
- Upgrade my server hardware
    
- Improve my network stack
    

---

## 😄 Final Thoughts

This project is a great example of why I enjoy running a homelab:

```text
You start with a simple idea,
and it turns into a full system involving networking,
data engineering, and visualization.
```

And at the end of it, you get something genuinely cool:

```text
A live view of the sky above your house.
```

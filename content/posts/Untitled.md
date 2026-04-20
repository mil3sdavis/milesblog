---
title: "From Panic to Pixels: Migrating My NAS and Recovering an Immich Library the Hard Way"
date: 2026-04-20
draft: false
tags:
  - blog
  - homelab
---
# From Panic to Pixels: Migrating My NAS and Recovering an Immich Library the Hard Way

I recently upgraded my homelab storage to a new NAS, and like any good plan, it worked perfectly… right up until it didn’t.

What started as a straightforward data migration turned into a deep dive into Docker, PostgreSQL, and how modern apps actually store data. In the end, I recovered everything—but not before learning a few lessons the hard way.

---

## The Goal

- Move ~6.5TB of data from an old Ubuntu-based NAS
    
- Stand up a new Unraid system (UGreen DXP4800 Plus)
    
- Migrate services like Plex and Immich cleanly
    

Simple enough… in theory.

---

## Step 1: Moving the Data

I used `rsync` over SSH to transfer everything:

```bash
rsync -avh --progress /old/media/ /mnt/user/media/
```

After fixing a bad Ethernet cable (don’t underestimate layer 1), I was getting ~100MB/s, and the transfer completed without issues.

---

## Step 2: Rebuilding the Stack

On the new NAS:

- Installed Unraid
    
- Set up shares (`media`, `appdata`)
    
- Deployed Immich using Docker Compose
    

Everything came up clean. Containers were running. UI loaded.

Then I opened Immich…

👉 **“Create Admin Account”**

---

## Step 3: The “Oh No” Moment

No photos. No albums. Nothing.

But I _knew_ the data was there.

That’s when I learned a critical truth:

> Apps like Immich don’t just read files—they rely heavily on a database.

---

## Step 4: Understanding Immich Storage

Immich doesn’t store photos in a human-readable way. Instead, it uses:

- Hashed directories
    
- UUID-based storage
    
- Metadata stored entirely in PostgreSQL
    

So while my files existed, they were effectively meaningless without the database.

---

## Step 5: Hunting Down the Database

I initially copied what I _thought_ was the database directory, but something felt off.

Eventually, I found the real one:

```bash
/home/miles/immich-app/postgres
```

From there, I:

1. Stopped the Immich stack
    
2. Wiped the new Postgres data directory
    
3. Copied the old database over with `rsync`
    
4. Fixed permissions (`chown -R 999:999`)
    
5. Restarted the stack
    

---

## Step 6: More Problems (Because of Course)

After restoring the DB:

- Containers started rebooting
    
- Postgres authentication kept failing
    

Turns out:

- The database had its own internal password
    
- My `.env` file didn’t match it
    

I had to reset the password inside Postgres to align everything.

---

## Step 7: The Unexpected Hero

After all that… Immich still showed a “Restore Database” option.

I clicked it (against my better judgment 😄)

👉 And it worked.

Immich had been quietly creating nightly backups of the database, and I was able to restore from one of those.

---

## Step 8: Everything Comes Back

Suddenly:

- Timeline populated
    
- Albums restored
    
- Metadata intact
    
- Face recognition data preserved
    

Total recovery.

---

## Lessons Learned

### 1. Files ≠ Data

Modern apps rely on databases. Without them, your files may be useless.

### 2. Always Migrate Database + Storage Together

If you move one without the other, things break in weird ways.

### 3. Check the _Actual_ Data Paths

Configs don’t always match reality. Verify where things really live.

### 4. Permissions Matter

Docker + Linux permissions can silently break everything.

### 5. Backups Are Everything

Immich’s built-in DB backups saved me. Period.

---

## What I’d Do Differently

- Backup the database explicitly before migrating
    
- Validate the DB path before copying
    
- Test restore before wiping the old system
    

---

## Final Thoughts

What started as a routine NAS upgrade turned into a full-on recovery exercise. But in the process, I gained a much deeper understanding of how my stack actually works.

And more importantly…

👉 I didn’t lose a single photo.

---

If you’re running services like Immich, Plex, or anything database-driven:

**Don’t just back up your files—back up your data.**
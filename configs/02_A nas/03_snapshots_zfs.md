# Setting Up Automatic Snapshots and ZFS Features

ZFS is one of the most powerful file systems and TrueNAS makes it easy to leverage its features, especially snapshots for data recovery.

## Creating Automatic Snapshots

1. Navigate to:  
   `Tasks` → `Periodic Snapshot Tasks`
2. Click **Add** and configure:
   - Pool/Dataset: Select the one to snapshot
   - Recursive: Enable if you want child datasets included
   - Schedule: Define frequency (e.g., daily, every 6 hours)
   - Lifetime: How long to retain snapshots (e.g., 7 days)
3. Save and enable the task.

## Restoring From a Snapshot

1. Go to:  
   `Storage` → `Snapshots`
2. Select a snapshot → Click **Clone to New Dataset** or **Rollback**

## ZFS Compression & Deduplication (Optional)

- Enable compression when creating a dataset (recommended: `lz4`)
- Deduplication is **not recommended** unless you have lots of RAM (16 GB+) and a specific use-case.

## Scrub Schedule

ZFS Scrubs help detect silent data corruption.

1. Go to:  
   `Tasks` → `Scrub Tasks`
2. Add a task for your pool and set frequency (e.g., monthly)

---


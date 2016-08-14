# WMFO Backups

## ZFS Backups

WMFO uses ZFS in a RAIDZ configuration for primary filestores. ZFS supports snapshotting, which can be done per-pool and saves exact state of the filesystem. These snapshots can then be synced between computers.

The current behavior is to snapshot daily and then send the delta to both the primary-backup and secondary-backup hosts.

All of these execute from Ringo's crontab.

## MySQL backups

MySQL backups need to be executed on all MySQL-hosting servers, including http and rivendell. They should be placed into the backup share on Ringo and then be replicated through the backup servers. These should ideally be versioned appropriately (hourly for 72 hours, daily for a month, monthly indefinitely).


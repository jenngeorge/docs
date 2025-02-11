---
title: Restoring Backups Across Versions
summary: CockroachDB's support policy for restoring backups across versions.
toc: true
docs_area: manage
---

This page describes the support Cockroach Labs provides for restoring backups across major versions of CockroachDB. The sections outline the support for the most common use cases when restoring backups across versions:

- [Support for restoring backups into a newer version](#support-for-restoring-backups-into-a-newer-version)
- [Support for long-term backup archival](#support-for-long-term-backup-archival)

{{site.data.alerts.callout_info}}
Since CockroachDB considers the cluster version when running a backup, this page refers to versions in a "v22.2.x" format. For example, both v22.2.8 and v22.2.14 are considered as v22.2 clusters for backup purposes.
{{site.data.alerts.end}}

{% include {{page.version.version}}/backups/recommend-backups-for-upgrade.md%} See [how to upgrade to the latest version of CockroachDB](upgrade-cockroach-version.html). 

## Support for restoring backups into a newer version

Cockroach Labs supports restoring a backup taken on a cluster on a specific major version into a cluster that is on the same version or the next major version. Therefore, when upgrading your cluster from version N to N+1, if you took a backup on major version N, you can restore it to your cluster on either major version N or N+1. Restoring backups outside major version N or N+1 is **not supported**. 

For example, backups taken on v22.1.x can be restored into v22.2.x. Backups taken on v22.2.x can be restored into v23.1.x. The following table outlines this support:

Backup taken on version   | Restorable into version
--------------------------+--------------------------
21.1.x                    | 21.1.x, 21.2.x
21.2.x                    | 21.2.x, 22.1.x
22.1.x                    | 22.1.x, 22.2.x
22.2.x                    | 22.2.x, 23.1.x

When a cluster is in a mixed-version state during an upgrade, [full cluster restores](restore.html#restore-a-cluster) will fail. See the [Upgrade documentation](../{{site.versions["stable"]}}/upgrade-cockroach-version.html) for the necessary steps to finalize your upgrade. For {{ site.data.products.db }} clusters, see the [Upgrade Policy](../cockroachcloud/upgrade-policy.html) page. 

{{site.data.alerts.callout_info}}
Cockroach Labs does **not** support restoring backups from a higher version into a lower version. 
{{site.data.alerts.end}}

## Support for long-term backup archival

When you need to archive a backup for the long term, we recommend that you also archive the CockroachDB binary of the version that the backup was taken on.

For a true archival copy that is not dependent on CockroachDB at all, running a changefeed to export your data from CockroachDB and archiving the files would be a better approach instead of taking a backup. See [Export Data with Changefeeds](export-data-with-changefeeds.html) for more detail.

## See also

- [`RESTORE`](restore.html)
- [Take Full and Incremental Backups](take-full-and-incremental-backups.html)
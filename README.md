# Exemplar Backup and Restore Release

This [BOSH](https://bosh.io/docs) release provides examples on how Cloud Foundry release authors can structure their jobs to implement the contract with BBR. This release is not intended to be a generic [exemplar release](https://github.com/cloudfoundry/exemplar-release).

Based on our experience with the current implementation of the backup and restore process for Cloud Foundry deployments, we have provided two example jobs to use as reference:

1. bbr-acme-db: This is intended to be collocated with the [BBR SDK release](https://github.com/pivotal-cf/backup-and-restore-sdk-release). This job needs to be on a VM that has persistent disk with sufficient space to store the backup artifact; the Backup-Restore VM instance can be used for this purpose. This job contains the actual backup and restore logic to be implemented by the release author.
1. acme-api: This component contains collocated lock and unlock scripts to enable the use of monit to start and stop component processes, should the component require locking during database backup. Note that the unlock script should be idempotent (as it may be called any number of times).

Note that these scripts can technically be placed on any VM in the deployment, but usually will be collocated with the component they are interacting with.

More information on the orchestration and contract between BBR and component scripts can be found in the [BBR Release Author Documentation](http://www.boshbackuprestore.io/bosh-backup-and-restore/release_author_guide.html)

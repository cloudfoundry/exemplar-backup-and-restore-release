# Exemplar Backup and Restore Release

This [BOSH](https://bosh.io/docs) release provides examples on how Cloud Foundry release authors can structure their jobs to implement the contract with BBR. This release is not intended to be a generic [exemplar release](https://github.com/cloudfoundry/exemplar-release). 

Based on our experience with the current implementation of the backup and restore process for Cloud Foundry deployments, we have provided two example jobs to use as reference:

1. Backup Restore Acme DB: This is intended to be collocated with the [BBR SDK release](https://github.com/pivotal-cf/backup-and-restore-sdk-release) on a Backup-Restore VM instance. It contains the actual backup and restore logic to be implemented by the release author.
1. Lock Unlock Acme DB: This job is intended to be collocated with the release author's component to enable the use of monit to start and stop component processes, should the component require locking during database backup.

More information on the orchestration and contract between BBR and component scripts can be found in the [BBR Release Author Documentation](http://www.boshbackuprestore.io/bosh-backup-and-restore/release_author_guide.html)

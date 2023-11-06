# Exemplar Backup and Restore Release

This [BOSH][bosh_docs] release provides examples on how Cloud Foundry release authors can structure their jobs to implement the contract with BBR. This release is not intended to be a generic [exemplar release][exemplar_release_repo].

[bosh_docs]: https://bosh.io/docs/
[exemplar_release_repo]: https://github.com/cloudfoundry/exemplar-release

Based on our experience with the current implementation of the backup and restore process for Cloud Foundry deployments, we have provided two example jobs to use as reference:

1. `bbr-acme-db`: This is intended to be collocated with the [BBR SDK release][bbr_sdk_repo]. This job needs to be on a VM that has persistent disk with sufficient space to store the backup artifact; the Backup-Restore VM instance can be used for this purpose. This job contains the actual backup and restore logic to be implemented by the release author. These exemplar backup and restore scripts will run with `bpm` isolation if colocated with the [BPM Release][bpm_release] and `bpm` is enabled, as documented in the [Transitioning to BPM Documentation][bpm_transitioning_docs].

2. `acme-api`: This component contains collocated lock and unlock scripts to enable the use of monit to start and stop component processes, should the component require locking during database backup. Note that the unlock script should be idempotent (as it may be called any number of times).

[bbr_sdk_repo]: https://github.com/cloudfoundry/backup-and-restore-sdk-release
[bpm_release]: https://github.com/cloudfoundry/bpm-release
[bpm_transitioning_docs]: https://github.com/cloudfoundry/bpm-release/blob/master/docs/transitioning.md#updating-deployment-manifest

Note that these scripts can technically be placed on any VM in the deployment, but usually will be collocated with the component they are interacting with.

Note that the BBR scripts in these example jobs depend upon the `release_level_backup` job property and run but do nothing if it is false; CF release authors should ensure that their BBR scripts follow this pattern.

More information on the orchestration and contract between BBR and component scripts can be found in the [BBR Release Author Documentation][bbr_devguide].

[bbr_devguide]: https://docs.cloudfoundry.org/bbr/bbr-devguide.html

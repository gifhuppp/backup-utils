# Getting started

 1. [Download the latest version of backup-utils][1] and extract the repository using `tar`:

    `tar -xzvf /path/to/github-backup-utils-vMAJOR.MINOR.PATCH.tar.gz`

    **Note**: you will need to use [Backup Utilities v2.11.x][2] or the `legacy` branch to
    backup and restore GitHub Enterprise Server 2.10 and earlier.

 2. Copy the [`backup.config-example`][3] file to `backup.config` and modify as
    necessary. The `GHE_HOSTNAME` value must be set to the primary GitHub Enterprise Server
    hostname. Additional options are available and documented in the
    configuration file but none are required for basic backup functionality.

    As the data on a High Availability replica may be in a transient state at the time of backup,
    Backup Utilities should not be used to backup data from a High Availability replica.

    * Backup Utilities will attempt to load the backup configuration from the following
      locations, in this order:

      ```bash
      $GHE_BACKUP_CONFIG (User configurable environment variable)
      $GHE_BACKUP_ROOT/backup.config (Root directory of backup-utils install)
      $HOME/.github-backup-utils/backup.config
      /etc/github-backup-utils/backup.config
      ```
    * In a clustering environment, the `GHE_EXTRA_SSH_OPTS` key must be configured
      with the `-i <abs path to private key>` SSH option.

 3. Add the backup host's SSH public key to the GitHub Enterprise Server appliance, in order to grant it administrative shell access.
    See [Accessing the GitHub Enterprise Server administrative shell (SSH)][4] for instructions.

 4. Run `bin/ghe-host-check` to verify SSH connectivity with the GitHub
    appliance.

 5. Run `bin/ghe-backup` to perform an initial full backup.

[1]: https://github.com/github/backup-utils/releases
[2]: https://github.com/github/backup-utils/releases/tag/v2.11.4
[3]: https://github.com/github/backup-utils/blob/master/docs/backup.config-example
[4]: https://docs.github.com/enterprise-server/admin/configuration/configuring-your-enterprise/accessing-the-administrative-shell-ssh

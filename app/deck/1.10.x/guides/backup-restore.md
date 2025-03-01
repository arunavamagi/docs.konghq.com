---
title: Backup and Restore of Kong's Configuration
---

You can use decK to back up and restore a subset or the entirety of
Kong's configuration.

To back up Kong's configuration, use the `dump` command:

```shell
$ deck dump
# this generates a kong.yaml file with the entire configuration of Kong
```

Then, restore this file back to Kong using the `sync` command:

```shell
$ deck diff # a dry-run where decK shows the changes it will perform
$ deck sync # actually re-creates the entities in Kong
```

## Manage a subset of configuration

You can export/import/manage a subset of Kong's configuration using decK's
`select-tag` feature. This is similar to adopting
[distributed configuration](/deck/{{page.kong_version}}/guides/distributed-configuration) for Kong.

The `select-tag` feature assumes that all the entities you would like to manage
in Kong share a common tag(s).

Assuming you have such a common tag (for example, let's call it `foo-tag`),
you can use it to export only a subset of the configuration:

```
deck dump --select-tag foo-tag
```

If you observe the file generated by decK, you will see the following section:

```yaml
_info:
  select_tags:
  - foo-tag
```

This subsection tells decK to filter out entities containing select-tags during
a sync operation.

Now, you can manage or sync back only this subset of Kong's configuration.

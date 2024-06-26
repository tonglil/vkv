---
hide:
  - toc
title: "vkv snapshot save"
---
## vkv snapshot save

create a snapshot of all visible KV engines recursively for all namespaces

```
vkv snapshot save [flags]
```

### Options

```
  -d, --destination string   vkv snapshot destination path (env: VKV_SNAPSHOT_SAVE_DESTINATION) (default "./vkv-snapshot-export")
  -h, --help                 help for save
  -n, --namespace string     namespaces from which to save recursively all visible KV engines (env: VKV_SNAPSHOT_SAVE_NS)
      --skip-errors          dont exit on errors (permission denied, deleted secrets) (env: VKV_SNAPSHOT_SAVE_SKIP_ERRORS)
```

### SEE ALSO

* [vkv snapshot](vkv_snapshot.md)	 - save or restore a snapshot of all KVv2 engines

###### Auto generated by spf13/cobra on 30-Apr-2024

# diff
`vkv` can be used to compare secrets across Vault servers or KV engines.

```bash
"diff -ty <(vkv export --p=secret --show-values) <(vkv export -p=secret_2 --show-values)"
```

Here is an example using `diff`, the `|` indicates the changed entry per line:

## Demo
![gif](assets/diff.gif)

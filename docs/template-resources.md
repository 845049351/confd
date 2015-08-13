# Template Resources

Template resources are written in TOML and define a single template resource.
Template resources are stored under the `/etc/confd/conf.d` directory by default.

### Required

* `dest` (string) - The target file.
* `keys` (array of strings) - An array of keys.
* `src` (string) - The relative path of a [configuration template](templates.md).

### Optional

* `group` (string) - The group name that should own the file.
* `mode` (string) - The permission mode of the file.
* `uid` (int) - The uid of the file.
* `gid` (int) - The gid of the file.
* `reload_cmd` (string) - The command to reload config.
* `check_cmd` (string) - The command to check config. Use `{{.src}}` to reference the rendered source template.
* `prefix` (string) - The string to prefix to keys.

## Example

```TOML
[template]
src = "nginx.conf.tmpl"
dest = "/etc/nginx/nginx.conf"
uid = 33
gid = 33
mode = "0644"
keys = [
  "/nginx",
]
check_cmd = "/usr/sbin/nginx -t -c {{.src}}"
reload_cmd = "/usr/sbin/service nginx restart"
```

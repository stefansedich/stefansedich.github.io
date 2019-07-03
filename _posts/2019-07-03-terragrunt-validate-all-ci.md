---
layout: post
comments: true
author: stefansedich
title: Terragrunt validate-all as part of your CI process
tags: ['terraform', 'terragrunt']
---
With the merging of [#761](https://github.com/gruntwork-io/terragrunt/pull/761) it is now possible to run `validate-all` with Terragrunt as part of your CI process without having to initialize the backend.

You can do this by setting the `remote_state.disable_init` configuration option. The easiest way to manage this is to use an environment variable that you set as part of your CI process to disable initialization:

```c
remote_state {
  disable_init = tobool(get_env("DISABLE_INIT", "false"))
}
```

Now when executing `validate-all` as part of your CI process with `DISABLE_INIT=true` Terragrunt will no longer attempt to initialize the backend before running Terraform validate.

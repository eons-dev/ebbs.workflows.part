# EBBS for GitHub

Have [ebbs](https://github.com/eons-dev/bin_ebbs) manage your git repo!

## Usage

### build/github.json
Make sure you have a valid EBBS github.json in the build folder of your directory. This would be something like:

```json
{
  "build_in" : "github",
  "clear_build_path" : true,
  "next": [
    {
      "build" : "publish",
      "run_when" : "release",
      "copy" : [
        {"../../inc/" : "inc/"}
      ],
      "config" : {
        "clear_build_path" : false,
        "visibility" : "public"
      }
    }
  ]
}
```


### Submodule

This repo should make up the entirety of your .github folder.

To get it there, clone this with [submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules):
```
git submodule add https://github.com/eons-dev/part_ebbs-workflows.git .github/workflows
```

## Features:

All ebbs workflows call your `build/github.json`.

### Activity Workflows

The following events trigger ebbs workflows:
 * "release"
 * "push"
 * "pull_request"

Any of those events can be used with the `"run_when"` json var, allowing you to use a single build.json for all your workflows.

For example:
```json
{
  "run_when": [
    "pull_request"
  ]
}
```

If you would like additional environment variables, cli args, build steps, etc, you can always clone this repo or modify the subrepo clone to your liking.

### Scheduled Workflows

The following scheduled events triggers are also available:
 * `"daily"` (runs at 0000 UTC)
 * `"weekly"` (runs at 0100 UTC)
 * `"monthly"` (runs at 0200 UTC)

Each scheduled trigger is set to run 1 hour after the preceding frequencies trigger so that any conflicting behavior can be executed with an order of known precedence. If your ebbs execution takes longer than 1 hour, let us know and we can multiply the offset.

### Automatic Updates

Coming soon!


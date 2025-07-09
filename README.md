# RenovateBot `packageManager` SHA512 issue repro

This is a minimal repo for a minimal repro of an issue I encountered with Renovate's automated update to the `packageManager` field in a few projects.

## The Issue

Renovate generated a PR which upgraded the `packageManger` field (the root-level one, used by `corepack`) as follows:

```
-   "packageManager": "pnpm@10.12.1+sha512.f0dda8580f0ee9481c5c79a1d927b9164f2c478e90992ad268bbb2465a736984391d6333d2c327913578b2804af33474ca554ba29c04a8b13060a717675ae3ac"
+   "packageManager": "pnpm@10.12.4"
```

Note the missing SHA512. As far as I can see, the hash is optional, but it caused the following error:

> ⚠️ Artifact update problem
>
> Renovate failed to update an artifact related to this branch. You probably do not want to merge this PR as-is.
>
> ♻ Renovate will retry this branch, including artifacts, only when one of the following happens:
>
> * any of the package files in this branch needs updating, or
> * the branch becomes conflicted, or
> * you click the rebase/retry checkbox if found above, or
> * you rename this PR's title to start with "rebase!" to trigger it manually
>
> The artifact failure details are included below:
>
> **File name: undefined**
>
> ```
> Command failed: corepack use pnpm@10.12.4
> ```

To work around this, I:

1. Cloned the repo locally
2. Ran `corepack use pnpm`

This updated the `packageManager` field to have the right hash and the PR proceeded as normal.


## Current status

Welp, RenovateBot got it right in this repo 🙃


## Example PR

https://github.com/lumphammer/shared-fvtt-bits/pull/206

This happened on more than one repo but this is the only public one.


## Discussion thread

https://github.com/renovatebot/renovate/discussions/36904

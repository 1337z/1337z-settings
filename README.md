# 1337z Settings

This GitHub App syncs repository settings defined in `.github/settings.yml` to GitHub, enabling Pull Requests for repository settings.

## Usage

This App is internal for the organisatzion 1337z.

### Inheritance

This app uses [probot-config](https://github.com/probot/probot-config). This means you can inherit settings from another repo, and only override what you want to change.

Individual settings in the arrays listed under `labels`, `teams` (once it is supported) and `branches` will be merged with the base repo if the `name` of an element in the array matches the `name` of an element in the corresponding array in the base repo. A possible future enhancement would be to make that work for the other settings arrays based on `username`, or `title`. This is not currently supported. 

To further clarify: Inheritance within the Protected Branches plugin allows you to override specific settings per branch. For example, your `.github` repo may set default protection on the `master` branch. You can then include `master` in your `branches` array, and only override the `required_approving_review_count`.
Alternatively, you might only have a branch like `develop` in your `branches` array, and would still get `master` protection from your base repo.

**WARNING:** Note that this app inherently _escalates anyone with `push` permissions to the **admin** role_, since they can push config settings to the `master` branch, which will be synced. In a future, we may add restrictions to allow changes to the config file to be merged only by specific people/teams, or those with **admin** access _(via a combination of protected branches, required statuses, and branch restrictions)_. Until then, use caution when merging PRs and adding collaborators.

Until restrictions are added in this app, one way to preserve admin/push permissions is to utilize the [GitHub CodeOwners feature](https://help.github.com/articles/about-codeowners/) to set one or more administrative users as the code owner of the `.github/settings.yml` file, and turn on "require code owner review" for the master branch. This does have the side effect of requiring code owner review for the entire branch, but helps preserve permission levels.

See [docs/deploy.md](docs/deploy.md) if you would like to run your own instance of this plugin.

## Dependencies

###This is build on top of https://github.com/probot/settings/

https://github.com/probot/settings/ is licensed with: `ISC`

>  ISC License
> 
> Copyright (c) 2017, Brandon Keepers
> 
> Permission to use, copy, modify, and/or distribute this software for any
> purpose with or without fee is hereby granted, provided that the above
> copyright notice and this permission notice appear in all copies.
> 
> THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
> WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
> MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
> ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
> WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
> ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
> OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

## License

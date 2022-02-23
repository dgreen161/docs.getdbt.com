---
title: "Understanding dbt Core versions"
id: "core-versions"
description: "Learn about semantic versions of dbt Core, and how long those versions are supported."
---

### Further reading
- To learn about the different ways you can install dbt Core, see "[How to install dbt Core](dbt-cli/install/overview)."
- To restrict your project to only work with a range of dbt Core versions, or use the currently running dbt Core version, see [`require-dbt-version`](require-dbt-version) and [`dbt_version`](dbt_version).
- To learn how you can use dbt Core versions in dbt Cloud, see "[Choosing a dbt Core version](cloud-choosing-a-dbt-version)."

dbt Core releases follow [semantic versioning](https://semver.org/). The policies and expectations on this page assume prior familiarity with semantic versions. If you're not familiar with semantic versions, we recommend that you start by reading the section titled ["What are semantic versions?"](#what-are-semantic-versions)

## Timeline and support

### Support for versions prior to v1.0

- We are no longer releasing new patches for minor versions prior to v1.0
- As of June 30, 2022, dbt Cloud will remove support for dbt Core versions older than v1.0

### Support for versions starting with v1.0

#### Minor version support

Minor versions will be supported for one year (12 months) from the date of their initial release. _This is a definite commitment._ Our mechanism for continuing to support a minor version is by releasing new patches for that minor version—so it's important to make sure you're always using the latest patch.

While a minor version is officially supported, you can use it in dbt Cloud. For more information, see ["Choosing a dbt version"](cloud-choosing-a-dbt-version).

#### Ongoing patches

During the 12 months of ongoing support, we will continue to release new patch versions that include fixes.

**Active Support:** In the first few months after a minor version's initial release, we will patch it with "bugfix" releases. These will include fixes for regressions and net-new bugs that were present in the minor version's original release.

**Critical Support:** When a newer minor version is available, we will transition the previous minor version into "Critical Support." Subsequent patches to that older minor version will be "security" releases only, limited to critical fixes related to security and installation.

After a minor version reaches the end of its critical support period, one year after its initial release, no new patches will be released.

#### Future versions

We aim to release a new minor "feature" every 3 months. _This is an indicative timeline ONLY._ For the latest information about upcoming releases, including their planned release dates and which features and fixes might be included in each, always consult the [`dbt-core` repository milestones](https://github.com/dbt-labs/dbt-core/milestones).

| dbt Core   | Initial Release | Latest Patch         | Active Support Until | Critical Support Until  |
|------------|-----------------|----------------------|----------------------|-----------------|
| 1.0.x      | 2021-12-03      | 1.0.1                | 1.1.0 release        | 2022-12-03      |
| _1.1.x_    | _2022-04_       |                      | _1.2.0 release_      | _2023-04_       |
| _1.2.x_    | _2022-07_       |                      | _1.3.0 release_      | _2023-07_       |
| _1.3.x_    | _2022-10_       |                      | _1.4.0 release_      | _2023-10_       |

_Italics: Future releases, NOT definite commitments. Shown for indication only._


## Expectations

What do we expect of dbt users, as we continue to release new versions of dbt Core?

### Upgrading to new patch versions

We expect users to upgrade to patches as soon as they're available. When we refer to a "minor version" of dbt Core, which may be written as v1.0 or v1.0.x, we are always referring to _the latest patch release of that minor version_. We highly encourage you to structure your development and production environments such that you can always install the latest patches of `dbt-core` and any adapter plugins (noting that those patch numbers may be different).

### Upgrading to new minor versions

You may continue to use any minor version of dbt while it is officially supported. While we do not expect users to immediately upgrade to newer minor versions as soon as they're available, there will always be some features and fixes that are only available for users of the latest minor version.

### Trying prereleases

All dbt Core versions are available as _prereleases_ before the final release. "Release candidates" are available for testing, in production-like environments, two weeks before the final release. For minor versions, we also aim to release one or more "betas," which include new features and invite community feedback, 4+ weeks before the final release. It is in your interest to help us test prereleases—we need your help!


## What are semantic versions?

Like many software projects, dbt Core releases follow [semantic versioning](https://semver.org/), which defines three types of version releases.

- **Major versions:** To date, dbt Core has had one major version release: v1.0.0. When v2.0.0 is released, it will introduce new features and break backwards compatibility for functionality that has been deprecated.
- **Minor versions**, also called "feature" releases, include a mix of new features, behind-the-scenes improvements, and changes to existing capabilities that are **backwards compatible** with previous minor versions. They will not break code in your project that relies on documented functionality.
- **Patch versions**, also called "bugfix" or "security" releases, include **fixes _only_**. These fixes could be needed to restore previous (documented) behavior, fix obvious shortcomings of new features, or offer critical fixes for security or installation issues. We are judicious about which fixes are included in patch releases, to minimize the surface area of changes.

### How we version adapter plugins

When you use dbt, you're using `dbt-core` together with an adapter plugin specific to your database. You can see the current list in ["Available adapters"](available-adapters). Both `dbt-core` and dbt adapter plugins follow semantic versioning.

`dbt-core` and adapter plugins coordinate new features and behind-the-scenes changes in minor releases. When it comes to fixing bugs, sooner is better—so patch versions are released independently for `dbt-core` and plugins.

What does that mean? Patch version numbers are likely to be different between `dbt-core` and the adapter plugin(s) you have installed. Major and minor version numbers should always match.

As an example, you may find you're using `dbt-core==1.0.3` with `dbt-snowflake==1.0.0`. The most important thing is that you're using the latest patch available for each (v1.0.x). If you're running dbt locally, you can use the `dbt --version` command to see which versions you have installed:
```
$ dbt --version
installed version: 1.0.3
   latest version: 1.0.3

Up to date!

Plugins:
  - snowflake: 1.0.0 - Up to date!
```
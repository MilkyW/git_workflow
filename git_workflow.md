# Git Workflow
#### 吴幸融 516030910253
## What?
![git-model](http://nvie.com/img/git-model@2x.png)

> **Git workflow** is a way to manage a project by *branching* and *merging* on Git.

## Why?

With Git, merging and branching are extremely cheap and simple, and they are considered one of the core parts of your daily workflow, really.

As a consequence of its simplicity and repetitive nature, branching and merging are no longer something to be afraid of. Version control tools are supposed to assist in branching/merging more than anything else.

## How?

> There are no iron rules of git workflow. The instructions from *Vincent Driessen* below is a common practice for your inspiration.

### Decentralized but centralized

![centr-decentr](http://nvie.com/img/centr-decentr@2x.png)

Each developer pulls and pushes to origin. But besides the centralized push-pull relationships, each developer may also pull changes from other peers to form sub teams. For example, this might be useful to work together with two or more developers on a big new feature, before pushing the work in progress to origin prematurely. In the figure above, there are subteams of Alice and Bob, Alice and David, and Clair and David.

Technically, this means nothing more than that Alice has defined a Git remote, named bob, pointing to Bob’s repository, and vice versa.

### The main branches 

At the core, the development model is greatly inspired by existing models out there. The central repo holds two main branches with an infinite lifetime:

`master`

`develop`

The `master` branch at `origin` should be familiar to every Git user. Parallel to the `master` branch, another branch exists called `develop`.

![main-branches](http://nvie.com/img/main-branches@2x.png)

We consider `origin/master` to be the main branch where the source code of `HEAD` always reflects a *production-ready* state.

We consider `origin/develop` to be the main branch where the source code of `HEAD` always reflects a state with the latest delivered development changes for the next release. Some would call this the “integration branch”. This is where any automatic nightly builds are built from.

When the source code in the `develop` branch reaches a stable point and is ready to be released, all of the changes should be merged back into `master` somehow and then tagged with a release number. How this is done in detail will be discussed further on.

Therefore, each time when changes are merged back into `master`, this is a new production release by *definition*. We tend to be very strict at this, so that theoretically, we could use a Git hook script to automatically build and roll-out our software to our production servers everytime there was a commit on `master`.

### Supporting branches 
Next to the main branches `master` and `develop`, our development model uses a variety of supporting branches to aid parallel development between team members, ease tracking of features, prepare for production releases and to assist in quickly fixing live production problems. Unlike the main branches, these branches always have a limited life time, since they will be removed eventually.

The different types of branches we may use are:

`Feature branches`

`Release branches`

`Hotfix branches`

Each of these branches have a specific purpose and are bound to strict rules as to which branches may be their originating branch and which branches must be their merge targets. We will walk through them in a minute.

By no means are these branches “special” from a technical perspective. The branch types are categorized by how we use them. They are of course plain old Git branches.

## References
[A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)
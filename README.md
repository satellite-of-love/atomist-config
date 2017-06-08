# atomist-config-seed

Atomist configuration repository for a GitHub organization.

## Structure

This repository contains configuration used by various aspects of the
Atomist system.  The files in the repository are managed by Atomist,
so you should not need to edit them but you can view them to get an
idea of how Atomist understands your repositories and their
relationships.

### Features

Features represent a unit of functionality in a project.  A feature
could be something like logging, database connectivity, or a
framework.

The `features.json` file manages how features flow between
repositories in your organization.  A single project can be a
broadcaster of a features while many projects could be a follower of
that feature in that project.  A given project could be the
broadcaster of many features.  A given project could also
simultaneously be a broadcaster of some features and a follower of
other features.

An example `features.json` file is below.

```json
{
    "broadcast": {
        "spring-rest-seed": {
            "features": [
                {
                    "name": "SpringBoot.Structure",
                    "followers": [
                        "demo10"
                    ]
                },
                {
                    "name": "baz",
                    "followers": []
                }
            ]
        }
    }
}
```

The top-level `broadcast` element has sub-elements for each broadcast
repository.  Each broadcast repository contains an array of
`features`, each having a `name` and a list of `followers`.

### Fingerprints

Fingerprints are simple strings that represent a snapshot of the
semantic structure of some aspect of your project.  For example, you
may wish to have a fingerprint for your public API.  The algorithm for
the fingerprint might read the annotations for methods defining
endpoints and create unique fingerprints for each possible API.  The
value of the fingerprint can be tracked from commit to commit.  If it
changes from one commit to the next, you have an indication that the
public API for your service has changed.

```json
{
    "repos": {
        "spring-rest-seed": [
            "Maven.+",
            "Spring.+"
        ],
        "$default$": [
            "Maven.+",
            "Spring.+"
        ]
    }
}
```

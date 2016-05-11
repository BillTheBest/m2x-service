# Instructions for filing issues

Please use the [m2x-service](https://github.com/attm2x/m2x-service) repository to fill any issues related to the M2X Service. If you want to file an issue for a client library refer to the corresponding project's repository. Be sure to search the list of open issues to see if your issue has already been raised.

Try to use distinct and descriptive subject lines to make issues easier to identify.

If you are filing a bug report, please include as much information/context as possible so we can understand what you tried to do and what went wrong by recreating the issue.

All feature requests and issues should be initially reported in the issues section of a repository. We are following the convention of naming an issue by prefixing its description with the issue type, as in "Feature Request: XXX", "Bug: XXX", or "UI: XXX".

# Contributing to our client libraries

Contributions to our client libraries are always welcome! We try to keep all our libraries up to date with the new features we release on M2X, but if you ever find a missing feature or want to contribute a bug fix or an enhancement we will happily review and accept it.

Please take a look at our [Contribution Guidelines](CLIENT-CONTRIBUTIONS.md) for instructions on which features the libraries are meant to support (not all M2X features will be supported by all client libraries).

Whether you are an internal or external contributor, the contribution procedure should be the same:

Each contribution should be made in its own branch. The branch name should follow this naming convention: `type/NNN-feature-name` where:

* `type` is either `feature`, `bug`, `fix`, `ui` or `refactor`;
* `NNN` is the issue number in GitHub; (If applicable)
* `feature-name` is a descriptive name for the feature you're working on.

Once you are done, open a new Pull Request and add a "Ready for Review" comment so we can take a look at it.

Members of the M2X team will take a look at the Pull Request as soon as possible and come up with suggestions (if any) until the Pull Request is approved.

Once the Pull Request is approved, internal contributors should merge it and delete the original branch. External contributions will be merged by the team member that approved the Pull Request.

Pull Requests should avoid changing the version number. Releases will be handled by the M2X team.

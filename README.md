# .github

## Code of Conduct

https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file

## .github/workflows

Reusable GitHub actions workflows for IATI.

### should_run.yaml

Determines if a deployment workflow should run for an IATI repository that uses dependabot dependency management for updates.

Pseudo Logic:

- If event_name = 'push', always run deployment
  - This covers any PRs/code pushed by a developer
  - PRs merged by dependabot don't pass this check
- If event_name = 'scheduled'
  - AND last commit author = dependabot (if last commit author is a developer, don't need to do another deploy because that commit would have triggered a deploy)
  - AND dependabot had a commit in last 24hrs (this is so we don't keep doing a deploy every day even if there are no new dependency updates)
  - Then run the deploy

### cd_example.yaml

Example of how to use `should_run.yaml` reusable workflow in your deployment workflow to control if it should run on nightly scheduled run.

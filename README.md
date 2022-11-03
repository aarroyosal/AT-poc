# Release Workflow

This workflow is based in gitflow model. We have 2 branches (main and stable). All features and regular fixes are added to the main branch via PR. Once a month a release will be made (see steps below). 
With the release, all the changes of the main branch will be pushed to the stable branch and a tag will be added to this branch. 

## Between releases
- PR names with conventional commits format (in case we use them in the future)
- The changelog for wach DW must be edited to add the new changes. The new changes will be added to the top section `## [Unreleased]` with the keep a changelog format
- The version file has to be updated with the changes, The version X.Y.Z will depend on the previous version and the new changes. For instance if previous version was 1.0.0 and only fixes has been added since last release, the new version will be 1.0.1, but if some features have been added, then the new version will be 1.1.0. To check the last released version you can see the changelog


## Start release workflow
- Go to Draft new release gh workflow in AT and manually launch it passing the version with the format yyyy-MM, for example, 2022-11. 
    - This workflow will create a PR from a release branch into stable branch
    - This workflow will deploy new versions to dedicated as well
    - Update changelog file manually in the release branch. In the changelog, update the section `## [Unreleased]` to `## [X.Y.Z] (yyyy-MM)`.
- Do the same step in ATC (this wf will not include the deploy to dedicated since it is not necessary there)
## QA
- 3-4 days for QA testing
    - If some bug raises during QA it can be fixed in this branch 

## Finish release
- Merge the release branch, this will trigger, a new workflow with the following steps:
    - Create a release in github and a tag with the version name
    - Publish the artifacts of the DW that have been updated 
    - Create a PR from stable to main branch
    - Launch workflow to update documentation (this could generate a PR that updates the documentation with the new reference)
- Merge the PR from stable to main (ATC finished)
- Merge the PR from stable to main and, if needed, update the ATC submodule (AT finished)
- Run release workflow in ATC. This will:
    - Create a tag with all the new versions 
    - Publish the core packages

# Hotfix Workflow
The hotfix workflows will be managed manually. following the next steps:
- Create a new branch with the format "hotfix/yyyy-MM-dd" from the base branch stable
- Add the fix to this new branch and create a PR to stable. 
- After testing and validating the fix, the PR can be merged, this will trigger the flow that publishes the new packages, create a release with a tag and create a PR to main.

# Next steps.
- Generate changelog dinamically based on commit messages. This can be done with this action https://github.com/marketplace/actions/release-changelog-builder and the help of an autolabeller like this https://github.com/marketplace/actions/labeler
- Check that the tag doesn't exist before starting the workflow
- Generate release body with DW versions
- Automatically merge the pull request from stable to main
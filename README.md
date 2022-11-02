# Release Workflow

## Between releases
- PR names with conventional commits format

## Start release workflow
- Go to Draft new release gh workflow in AT and manually launch it passing the version with the format yyyy-MM, for example, 2022-11. 
    - This workflow will create a PR from a release branch into stable branch
    - This workflow will deploy new versions to dedicated as well
    - Update changelog manually?

## QA
- 3-4 days for QA testing
    - If some bug raises during QA it can be fixed in this branch 

## Finish release
- Merge the release branch, this will trigger, a new workflow with the following steps:
    - Create a release in github and a tag with the version name
    - Publish the artifacts of the DW that have been updated 
    - Create a PR from stable to main branch
    - Launch workflow to update documentation (this could generate a PR that updates the documentation with the new reference)
- Merge the PR from stable to main (AT finished)
- Run the draft new release workflow in ATC, and merge it (this wf will not include the deploy to dedicated since it is not necessary there)
- Run release workflow in ATC. This will:
    - Create a tag with all the new versions 
    - Publish the core packages

# Hotfix Workflow
The hotfix workflows will be managed manually. following the next steps:
- Create a new branch with the format "hotfix/yyyy-MM-dd" from the base branch stable
- Add the fix to this new branch and create a PR to stable. 
- After testing and validating the fix, the PR can be merged, this will trigger the flow that publishes the new packages, create a release with a tag and create a PR to main.

# Next steps.
Generate changelog dinamically based on commit messages. This can be done with this action https://github.com/marketplace/actions/release-changelog-builder and the help of an autolabeller like this https://github.com/marketplace/actions/labeler
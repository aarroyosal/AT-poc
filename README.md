# AT-poc

## Between releases
- PR names with conventional commits notation

## Start release workflow
- Go to pre-release gh workflow in AT and manually launch it. 
    - This workflow will create a PR from a release branch updating the changelogs for each WH and updating versions
    - This version will deploy to dedicated as well

## QA
- 3-4 days for QA testing
    - If some bug raises during QA it can be fixed in this branch 

## Finish release
- Run pre-release in ATC **If we release ATC now, when do we update the core submodule? we can leave it to where it was at the moment, but perhaps is better to update the reference to point at a tag**
- Merge the ATC release PR in main
- Run release workflow in ATC. This will:
    - Create a tag with all the new versions (bq-v1.0.0, sf-v1.0.0, etc)
    - Publish the packages
- Merge the AT release PR in main
- Run release workflow in AT. This will:
    - Create a tag with all the new versions (bq-v1.0.0, sf-v1.0.0, etc)
    - Publish the packages **At this point the complete changelog (AT + ATC) could be created but for this, the ATC has to be released before the AT release starts. This might be done manually by joining the 2 changelogs**
    - Launch workflow to update documentation (this could generate a PR that updates the documentation with the new reference)
    - Remove dedicated AT



# Issues
 Big problem found when features are pushed into main branch after after the PR is created this is because 
 T∫his may be fixed by initiating the process after the tag is created

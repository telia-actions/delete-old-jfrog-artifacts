
# Delete old artifacts from JFrog repository

This action is for deleting old artifacts in a given JFrog repository (for example, when JFrog repository storage limit warning level is reached).

## Inputs

### jfrog-repo-name:
Name of JFrog repository to delete old artifacts from. **Required**
### jfrog-username:
JFrog username to use for deleting old artifacts. Should have WRITE permissions. **Required**
### jfrog-password:
JFrog user password.
### artifact-prefix-to-search:
Prefix of the artifacts to check. Default value 'Telia'. **Required**
### limit-of-months:
Limit of months how old should be the artifact to be deleted. Default value is 6. **Required**
### minimum-number-of-artifacts-to-leave:
Minimum number of artifacts to leave even if they are old. This is a precautionary parameter to prevent deleting latest old artifacts as they might be the ones currently deployed. Default value is 100. **Required**


## Example

```
    name: Clean JFrog repository
    
    on:
      workflow_dispatch:
    
    jobs:
      delete-old-artifacts:
        runs-on: [ec2, windows, medium]
        name: Delete old artifacts from JFrog repository
        steps:
          - uses: telia-actions/delete-old-jfrog-artifacts@v1
            with:
              jfrog-repo-name: 'some-jfrog-repo-name'
              jfrog-username: ${{ vars.JFROG_USERNAME }}
              jfrog-password: ${{ secrets.JFROG_PASSWORD }}
              artifact-prefix-to-search: 'some-specific-artifact-prefix'
```

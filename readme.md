This is meant to accompany the second 'Developer Handbook' presentation where I get into the details of this altered Gitflow model

### Stage 1: Project Starts
- it is too cumbersome to merge request for every commit because you don’t have anything built yet
- instead we start an unprotected branch called ‘develop’
- since it’s unprotected anyone can push to it on gitlab
- remember to follow the ‘Commit Message’ guidelines on every branch including this one
- see FEATURE/BUG/REFACTOR/MISC commits as in the last presentation
- [See it in action](stage1.md)

### Stage 2: Staging
- we introduce the ‘master’ branch which will be deployed to staging server
- master branch is protected so to push code to it you have to issue a merge request which needs to be assigned to a senior developer on the project, if no senior developer exists assign it to me
- at this point you should start using FEATURE and BUG branches
- add capistrano-revisions gem so the PM is notified each time you deploy something to the staging server
- if you are working on a feature and find a problem with it, commit your fix on the feature branch, not directly to the develop branch, this keeps all the code together in a single branch that can be squashed to a single commit
- master always contains working/shippable code, if the code is not working/shippable at this time you can keep it in develop branch but you have to remove it from master branch
- merge bug fixes you discover on master branch back to develop branch
- features are based off develop branch
- merge features/bug fixes from develop branch to master branch
- [See it in action](stage2.md)

### Stage 3: Production
- now you have a staging and a production server
- introduce a new branch called staging
- mark staging branch as protected in gitlab
- since it's protected you have to issue merge requests to push code to it
- configure capistrano-revisions to use the production environment too so you get deployment notifications both for production and staging servers
- master branch now becomes production ready code
- staging branch is what’s deployed to staging server
- role of develop branch stays the same
- staging branch may get push forced so don’t store your code there
- if a feature needs to be disabled keep your code in develop branch
- create hotfix brances off master branch if you need to fix something on production and merge them back into staging branch
- merge back your hotfix into develop too
- everything needs to come back to develop since it becomes the new staging at the beginning of every sprint and staging becomes the new master eventually
- at the end of each sprint staging should be
 - tested
 - merged into master
 - deployed to production server
 - tagged with a redmine sprint #
- when a new sprint begins push force develop to staging branch
- [See it in action](stage3.md)

### Merge requests
- if you get a merge request assigned to you examine the code, see if it makes sense, if it doesn’t then make a comment on gitlab and reject it
- verify the build is passing before approving merge requests, if it’s failing, get it fixed first, do not approve merge requests that fail to bulid
 - rspec must pass
 - integration spec must pass
 - rubocop must pass
- if it’s failing create an issue for the developer to fix the build
- if it makes sense and the build passes, approve the merge request and mark the remote branch for deletion after merge request is complete

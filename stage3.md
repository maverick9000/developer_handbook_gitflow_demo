assume we have a production server setup and we can issue ‘cap production deploy’

```shell
# create staging branch on gitlab and mark it as protected
git checkout develop
git checkout -b staging
git push -u origin staging
# now staging branch is deployed to staging and master branch is deployed to production
# everything is same as before but now you also have hotfix branches for when you discover a problem on production
# create issue on redmine
git checkout master
git pull
git checkout -b hotfix/5454_fix_email
echo 'some code' > fix2.rb
git add .
git commit
# BUG #5454 - Fix email
git push -u origin hotfix/5454_fix_email
# create merge request
# once merged
cap production deploy
# marge it back to staging
git checkout staging
git merge master
# merge it back to deploy
git checkout deploy
git merge master
# when sprint ends
git checkout staging
git pull
# make sure it's tested, spec passes, rubocop passes, have senior dev do the merge
git checkout master
git merge staging
git tag 1.0 #sprint number
cap production deploy
# once new sprint begins restart staging branch from develop
git checkout develop
git pull
git checkout staging
git reset --hard develop
git push origin staging --force
```

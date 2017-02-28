assume staging server is already created and we can just issue ‘cap staging deploy’

```shell
# create master branch and protect it
# set master branch as default
git checkout master
# work on feature
git checkout develop
git checkout -b feature/4324_forgot_password
echo 'some code' > feature2.rb
git add .
git commit
# FEATURE #4324 - Add 'Forgot password'
git push -u origin feature/4324_forgot_password
# do another commit
echo 'some code' > feature3.rb
git add .
git commit
# FEATURE #4324 - Add 'Forgot password' feature
#
# - change spelling
git push
# since this feature is complete, ready to create merge request to put it on staging so it can de delpoyed
# create merge request
# go through accepting merge request
# examine code
cap staging deploy
```

```shell
# what if you find a bug on staging?
# create issue on redmine
git checkout master
git pull #other people may have pushed
git checkout -b bug/4355_fix_forgot_password
echo 'some code' > bug.rb
git add .
git commit
# BUG #4355 - fix forgot password
git push -u origin bug/4355_fix_forgot_password
# create merge request
# once it's merged to master, deploy it
cap staging deploy
# and merge it back into develop branch
git checkout develop
git merge master
```

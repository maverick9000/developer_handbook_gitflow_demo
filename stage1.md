```shell
# create test repository on gitlab
# create develop branch and allow anyone to push to it
```

```shell
git clone gitlab@gitlab.ekohe.com:ekohe/test.git
cd test
git checkout -b develop
echo 'readme' > README.md
git add .
git commit
# initial commit
git push -u origin develop
```

```shell
# create redmine project
# create sprint 1
# create feature
# confirm you are in develop branch
echo 'some code' > feature.rb
git add .
git commit
# FEATURE #23423 - User registration
git push
```

```shell
# you discover a bug
# create issue on redmine
# confirm you are in develop branch
echo 'some code' > fix.rb
git add .
git commit
# BUG #234234 - Fix user registration
git push
```

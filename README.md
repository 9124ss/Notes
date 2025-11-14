Useful snippets

Git Checkout Remote Branch

------------
First, fetch the remote branches:

git fetch origin 
Next, checkout the branch you want. In this case, the branch we want is called “branchxyz.”

git checkout -b branchxyz origin/branchxyz 

--------
Merge main onto you branch:

git checkout final-summary
git pull --rebase origin main
git log --oneline --graph --branches -30
git push --force-with-lease

--------

Change and check remote URL

--------

[alias] start-ticket = "!f() { if [ -z "$1" ] || [ -z "$2" ]; then echo "Missing branch name and/or MR title"; exit 1; fi; b=$(echo 
1 | tra -zA - Z);t=(echo $b | sed -E 's/([0-9])/-\1/'); git checkout -b $1 && git push -o merge_request.create -o merge_request.title="WIP: $t: $2" -u origin head; }; f"

git start-ticket jira123 "Add more foo to the bars"

Which will create a branch named jira123, and an MR titled WIP: JIRA-123: Add more foo to the bars.

---------

globally ignore *.iml

git config --global core.excludesfile ~/.gitignore_global
touch ~/.gitignore_global
echo "*.iml" >> ~/.gitignore_global


----------
Show latest differences

git log -p -1 HEAD

------
git branch -avv

//refresh branches git remote update origin --prune

git fetch --prune

git reset --hard src/test/resources/features/date-of/changes.feature

git reset HEAD src/test/resources/features/date-of/changes.feature

------

Merge main onto you branch:

git checkout main
git pull --rebase 
git checkout final-summary
git rebase main
git log --oneline --graph --branches -30
git push --force-with-lease

----------

Squash commit on your branch using 's' on the lines that are to squash

git rebase -i main
git rebase --abort
git log --oneline --graph --branches -30
git rebase -i 2cb786e
code src/test/java/agent/ui/pages/TaskListPage.java
git add -u
git status
git rebase --continue
git branch -avv
git push --force-with-lease
git log --oneline --graph --branches -30

------

Git Checkout Remote Branch

First, fetch the remote branches:

git fetch origin 
Next, checkout the branch you want. In this case, the branch we want is called “branchxyz.”

git checkout -b branchxyz origin/branchxyz 
-------

run maven tests
mvn clean test -U -Dexec.skip=true -Denv=local -Dbrowser=htmlunit -Dcucumber.options="--tags 'not @ignore'" -Dno.fail.fast

---------

backward compability test id cit-ui and cla-service

./up.sh --clean
docker ps -a | grep cit
 #remove cit-ui and cla-service
docker stop 0f25b2c6c07d 315e07ac3f28
docker ps -a | grep cit
docker rm 0f25b2c6c07d 315e07ac3f28
docker ps -a | grep cit
TAG_CIT_UI=snapshot-jira192-epic TAG_CLA_SERVICE=snapshot-jira192-epic docker-compose up -d cla-service cit-ui
docker ps -a | grep apply
---------

Clean up docker

docker system prune --all
docker network ls
docker ps
docker container rm <id>

--------

Using a local docker build

# Clean up
docker-compose down --volumes && rm -rf pgdata
# Bring up old service

TAG_DIST_UI=0.1.2 \
TAG_CLA_SERVICE=0.3.2 \
./up.sh
# Manually build the cit one
cd cit-ui
git checkout 0.3.2
docker build -t cit-ui --build-arg NPM_REGISTRY_URL=$(npm get registry) -f docker/Dockerfile .
# Edit docker-compose.yml to use local image
# Bring up
docker-compose kill cit-ui
docker-compose up -d cit-ui

Editing docker-compose.yml to use local image:

cit-ui:
    # image: "xxx.dkr.ecr.eu-west-2.amazonaws.com/xxx/xx/cit-ui:${CIT_UI}"
    image: cit-ui

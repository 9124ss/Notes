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


# We're using Java from Homebrew, so installation locations will be custom
# ref: https://mkyong.com/java/how-to-install-java-on-mac-osx/#homebrew-install-java-8-on-macos

# Can't do this due to privileges:
# sudo ln -sfn $HOME/.homebrew/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk
JAVAPREFIX_16="$(brew --prefix)/opt/openjdk@16"
JAVAPREFIX_LATEST="$(brew --prefix)/opt/openjdk"

# Switch between Java versions here
# Useful ref: https://www.baeldung.com/maven-java-home-jdk-jre
JAVAPREFIX="$JAVAPREFIX_LATEST"
export JAVA_HOME="$JAVAPREFIX"
export PATH="$JAVAPREFIX/bin:$PATH"

----------


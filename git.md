# Git

#### Create new github repo from local

Add this function to `.bash_profile`

```bash
#Github new repo
github-create() {
  repo_name=$1

  dir_name=`basename $(pwd)`

  if [ "$repo_name" = "" ]; then
  echo "Repo name (hit enter to use '$dir_name')?"
  read repo_name
  fi

  if [ "$repo_name" = "" ]; then
  repo_name=$dir_name
  fi

  invalid_credentials=0

  username=`git config github.user`
  if [ "$username" = "" ]; then
  echo "Could not find username, run 'git config --global github.user <username>'"
  invalid_credentials=1
  fi

  token=`git config github.token`
  if [ "$token" = "" ]; then
  echo "Could not find token, run 'git config --global github.token <token>'"
  invalid_credentials=1
  fi

  if [ "$invalid_credentials" == "1" ]; then
  echo "Errors '$invalid_credentials'"
  return 1
  fi

  echo -n "Creating Github repository '$repo_name' ..."
  curl -u "$username:$token" https://api.github.com/user/repos -d '{"name":"'$repo_name'"}' > /dev/null 2>&1
  echo " done."

  echo -n "Pushing local code to remote ..."
  git remote add origin git@github.com:$username/$repo_name.git > /dev/null 2>&1
  git push -u origin master > /dev/null 2>&1
  echo " done."
}
```

#### Create pull request from command line

```bash
pr = "!f() {\
 remote=`git rmv | grep origin | grep push | awk '{print $2}'`;\
 project=`echo $remote | awk -F/ '{ print $(NF-1) }'`;\
 repo=`echo $remote | awk -F/ '{ print $NF }' | cut -d. -f1`;\
 branch=`git rev-parse --abbrev-ref HEAD`;\
 browser=chrome;\
 case $1 in\
  github | gh) open https://github.com/$project/$repo/compare/$branch...develop?expand=1;;\
  gitlab | gl) open https://gitlab.com/$project/$repo/merge_requests/new?merge_request[source_branch]=$branch;;\
  bitbucket | bb) open https://bitbucket.org/$project/$repo/pull-requests/new;;\
  echo) echo https://host:port/path/$project/$repo?branch=$branch;;\
 esac;\
}; f"
```

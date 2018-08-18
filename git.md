# Git

1. [System setup](#system-setup)
2. Repository setup
   * Remote repository
3. Branch
4. Merge

## System setup
#### Set your username
```shell
$ git config --global user.name "Your name"
```
#### Set your email
```shell
$ git config --global user.email your.name@email.com
```
#### Save credentials
```shell
$ git config credential.helper store
```

<br>
<div align="right">
    <b><a href="#git">↥ back to top</a></b>
</div>
<br>

## Repository setup
#### Navigate to the root directory of the app and initialize a new repository
```shell
$ git init
```
#### Add ALL projects files to the repository
```shell
$ git add -A
```
#### Commit in order to keep the changes
```shell
$ git commit -m "Initialize repository"
```

<br>
<div align="right">
    [↥ back to top](#git")
</div>
<br>
---
title: 检查git develop分支是否合入master分支
date: 2023-05-23 11:13:23
tags: Git
categories: 随笔
link: check-git-devin-master
---
## 脚本使用方式：

sh 脚本 $1 $2

检查 $2 是否最后一次commit是否执行合入到$1

eg：sh check_master_mr.sh master develop

<!-- more -->

```#!/bin/sh
merge_destination_branch=$1
merge_source_branch=$2

merge_base=$(git merge-base $merge_destination_branch $merge_source_branch)
merge_source_current_commit=$(git rev-parse $merge_source_branch)
if [[ $merge_base = $merge_source_current_commit ]]
then
    echo $merge_source_branch is merged into $merge_destination_branch
    exit 0
else
    echo $merge_source_branch is not merged into $merge_destination_branch
    exit 1
fi
```



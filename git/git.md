# git

<https://www.coursera.org/learn/version-control-with-git>

The Final Project is in fact not graded - I completed the course with 100% completing the quizzes and the final exam before I completed
the Final Project (and had to access the course from my Completed Courses to get to the Final Project).

Because of this, I judge it be sound to present my solution to this project. This is a step by step example for learners to imitate,
and it is longer than most worked out examples that appear at the top of many search engine results.

<img width="1197" height="573" alt="git image: © Atlassian" src="https://github.com/user-attachments/assets/8679aeba-f0b6-49cc-a4ae-6a70bf1a0b03" />

<img width="1202" height="787" alt="image: © Atlassian" src="https://github.com/user-attachments/assets/dbbcf131-ead4-48c3-980a-caa9caa5b99c" />


I made this working on Git Bash: <https://www.atlassian.com/git/tutorials/git-bash>

In the terminal (Git Bash, or a native Unix type terminal), change working directory to
any directory `X` such that `X/FinalProject` does not exist.
Save the below code block as `Y.sh` for any `Y`, and execute `bash Y.sh`.
A directory `X/FinalProject` is created that is a git repository with the given
commit history.

```bash
#!/bin/bash

# A
git init FinalProject
cd FinalProject
echo "# Readme v1.00" > README.md
git add README.md
git commit -m "add README.md"

# B
git checkout -b develop
touch fileA.txt
git add fileA.txt
git commit -m "add fileA.txt"

# C
git checkout -b feature1
echo "feature 1 wip" >| fileA.txt
git add fileA.txt
git commit -m "feature 1 wip"

# D
echo "feature 1 with 2 bugs" >| fileA.txt
git add fileA.txt
git commit -m "add feature 1"

# E
git checkout develop
git merge feature1
git commit -m "Merge branch 'feature1' into develop"

# F
git checkout -b feature2
echo "feature 2 wip" >> fileA.txt
git add fileA.txt
git commit -m "feature 2 wip"

# G
git checkout -b release1
echo "feature 1 with 1 bug" >| fileA.txt
git add fileA.txt
git commit -m "fix feature 1 bug X"

# H
git checkout master
git merge release1
git tag -a -m "Merge branch 'release1'" v1.00

# I
git checkout develop
git merge release1
git commit -m "Merge branch 'release1' into develop"

# F1
git checkout feature2
git rebase master
git commit -m "feature 2 wip"

# K
git checkout -b hotfix1
echo "feature 1" >| fileA.txt
git add fileA.txt
git commit -m "fix feature 1 bug Y"

# L
git checkout master
git merge hotfix1
git tag -a -m "Merge branch 'hotfix1'" v1.01

# M
git checkout develop
git merge hotfix1
git commit -m "Merge branch 'hotfix1' into develop"

# F2
git checkout feature2
git rebase master
```

<img width="1237" height="692" alt="© Atlassian" src="https://github.com/user-attachments/assets/1677671b-be64-4c8f-9c6b-4946a365dfa4" />


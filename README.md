# 2025-may-softuni-git-11-put-it-all-together

1. Cloning remote repo

![1-clone-remote](./readme-files/1-clone-remote.png)

2. Initializing java maven project with dependencies and plugins
![2-maven-spotless-check](./readme-files/2-maven-spotless-check.png)
![2-maven-tests](./readme-files/2-maven-tests.png)

3. Adding git hooks to check formatting and run tests:

	 .git/pre-commit code formatting hook:

```
#!/bin/sh

echo "Running spotless check on formatting ..."

mvn spotless:check

if [ $? -ne 0 ]; then 
	echo "Code needs additional formatting. Run mvn spotless:apply to re-format. Commit aborted"
	exit 1
fi

echo "Code up to standard"
	
```

![03-pre-commit-format-check.png](./readme-files/03-pre-commit-format-check.png)

![03-pre-commit-hook-formatted](./readme-files/03-pre-commit-hook-formatted.png)

.git/hooks/pre-push to run tests: 

```
#!/bin/sh

echo "Running tests"

mvn test

if [ $? -ne 0 ]; then
	echo "Push aborted tests failes"
	exit 1
fi

echo "Tests succeeded comencing push"
```

![03-pushing-with-failing-tests-1.png](./readme-files/03-pushing-with-failing-tests-1.png)
![03-pushing-with-failing-tests-2.png](./readme-files/03-pushing-with-failing-tests-2.png)

4. Rebasing feature-branch onto main with push --force-with-lease to push new history to remote

![04-rebasing-feature-onto-main-with-force-push-to-remote.png](./readme-files/04-rebasing-feature-onto-main-with-force-push-to-remote.png)

5. Adding GitHub Actions and triggering them on push to remote
   1. firstly malformatted yaml configuration
   2. second push verifies maven project - runs tests as action
   
![05-github-actions.png](./readme-files/05-github-actions.png)

6. Merge and clean-up of feature-branch

![06-main-merge-feature-branch.png](./readme-files/06-main-merge-feature-branch.png)
![06-main-merge-feature-branch-clean-up.png](./readme-files/06-main-merge-feature-branch-clean-up.png)
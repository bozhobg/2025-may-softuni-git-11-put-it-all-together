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

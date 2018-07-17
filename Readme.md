gitlab-sonar-scanner
====================
Available environment variables
-------------------------------

Can be checked in the official documentation: https://docs.sonarqube.org/display/SONARQUBE43/Analysis+Parameters

- `SONAR_URL`
- `SONAR_PROJECT_VERSION`
- `SONAR_DEBUG`
- `SONAR_SOURCES`
- `SONAR_PROFILE`
- `SONAR_LANGUAGE`
- `SONAR_PROJECT_NAME`
- `SONAR_BRANCH`
- `SONAR_ANALYSIS_MODE`

### sonar-gitlab specific
- make sure your Gitlab project has a secret variable (project -> settings -> CI/CD) defined called `SONAR_TOKEN` (it used for login.
- `SONAR_GITLAB_PROJECT_ID`: The unique id, path with namespace, name with namespace,
  web url, ssh url or http url of the current project that GitLab.
- `CI_COMMIT_SHA`: The commit revision for which project is built
- `CI_COMMIT_REF_NAME`: The branch or tag name for which project is built

### Defining custom sonar-scanner options

You can pass any additional option to the `sonar-scanner-run` binnary, if needed:

~~~yaml
sonarqube-reports:
  image: raserge/gitlab-sonar-scanner
  variables:
    SONAR_URL: http://your.sonarqube.server
    SONAR_ANALYSIS_MODE: publish
  script:
  - sonar-scanner-run -Dsonar.host.url=$SONAR_URL -Dsonar.login=$SONARQUBE_TOKEN -Dsonar.projectVersion=$CI_JOB_ID -Dsonar.branch=$CI_COMMIT_REF_NAME
~~~

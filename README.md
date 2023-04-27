# project-validation-action

This action is intended to share a common set of steps we use to
validate the quality of a project.

- Checkout the code
- Start Sonar
- Run the tests
- Stop Sonar and publish it's results
- Publish test results

## Parameters

#### 'sonar-project-name' (required)
The name of the Sonar project so we can publish
the results to the right place.

#### 'sonar-tool-version' (optional)
The Sonar tool version we install for this run. Default 
is 5.8.0 but this param will allow one to override if
needed.

#### 'sonar-token' (required)
The secret Sonar token for authenticating with Sonar.

#### 'github-token' (required)
The secret Github token for authenticating with Github.

#### 'aws-access-key-id' (required)
The AWS access key id, should always be for dev.

#### 'aws-secret-access-key' (required)
The AWS secret access key, should always be for dev.

#### 'use-dependencies' (optional)
Tests can be ran with dependencies if needed. Dependencies
can be defined in a docker compose file. And this switch
can turn on the behavior to ensure the dependencies are 
started. This is off by default.

#### 'docker-compose-file-path' (optional)
This parameter tells the action where to find the 
Docker compose file that defines the dependencies
needed. Default is 'docker-compose/test-dependencies-compose.yml'

#### 'path-to-repo-root' (optional)
This parameter helps docker containers access local files in the repo.

## Sample Use

```
project-validation:
  needs: [ alert-action-started ]
  name: "Validate Project Quality"
  runs-on: psidev-linux
  steps:
  - uses: patriotsoftware/project-validation-action@v1
    with:
      sonar-project-name: SynergyDataSystems_PatriotSoftware.Time
      sonar-token: ${{ secrets.SONAR_TOKEN }}
      use-dependencies: 'true'
      github-token: ${{ secrets.GITHUB_TOKEN }}
      aws-access-key-id: ${{ secrets.DEV_AWS_ACCESS_KEY_ID }}
      aws-secret-access-key: ${{ secrets.DEV_AWS_SECRET_ACCESS_KEY }}
```

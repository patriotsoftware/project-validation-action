# project-validation-action

This action is intended to share a common set of steps we use to
validate the quality of a project on SonarQube.

- Checkout the code
- Start Sonar
- Run the tests
- Stop Sonar and publish it's results
- Publish test results

## Parameters

#### 'github-repo-name' (required)
The name of the GitHub repo name.

#### 'sonar-tool-version' (optional)
The Sonar tool version we install for this run. Default 
is 5.8.0 but this param will allow one to override if
needed.

#### 'use-dependencies' (optional)
Tests can be ran with dependencies if needed. Dependencies
can be defined in a docker compose file. And this switch
can turn on the behavior to ensure the dependencies are 
started. This is off by default.

#### 'docker-compose-file-path' (optional)
This parameter tells the action where to find the 
Docker compose file that defines the dependencies
needed. Default is 'docker-compose/test-dependencies-compose.yml'

#### 'sonar-token' (required)
The secret Sonar token for authenticating with Sonar.

#### 'path-to-repo-root' (optional)
This parameter helps docker containers access local files in the repo.

#### 'tests-path' (optional)
The path to .NET tests by default is 'test/'

#### 'dotnet-test-command-args' (optional)
Arguments set on 'dotnet test' command arguments

#### 'local-runsettings-filename' (optional)
Full 'local.runsettings' file path, use NONE when file not required

#### 'upload-sonar-results' (optional)
This parameter controls whether to upload Sonar results as an artifact.
default is '--filter TestCategory!="Smoke"'

#### 'fail-on-failure' (optional)
Quality Gate will turn red and fail. Set to 'true' by default.  

#### 'ignore-failures' (optional)
When value is 'sonar' it will ignore the Sonar Quality Gate

#### 'vulnerability_codes' (optional)
Pipe delimited vulnerabilities to look for on build.log output

## Sample Use

```
  project-validation:
    name: "Sonar Validate Project Quality"
    runs-on: psidev-linux
    steps:
    - uses: patriotsoftware/project-validation-action@v1.1
      with:
        sonar-token: ${{ secrets.SONAR_TOKEN }}
        github-repo-name: ${{ github.event.repository.name }}   
```

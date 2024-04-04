# github-actions

This repository goes over GitHub actions and runs a script based on this created action.

## YAML Syntax

```main.yml``` - main configuration file for action

### Keys

```name``` - The name of the GitHub Action.
```
name: My GitHub Action
```

```on``` - The set of conditions that runs this action.
```
on:
  push:
    branches:
      - main
```

```env``` - A list of environment variables that the action will use throughout the run.
```
env:
  ENV: dev
  USER: root
  PASS: password
```

```defaults``` - A mapping of default settings that will be applied to all jobs.

```jobs``` - A list of the various jobs the action will do.

#### ```on``` Syntax

- ```on.push.<branches|tags>``` 

  - Will trigger action when anything is pushed to the repository. Can narrow down trigger by specifying the branch or tag to be monitored.

  ```
    on:
      push:
        branches:
          - main
  ```

- ```on.<event_name>.types``` 

  - Will trigger action when any of [these events](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#available-events) are modified

  ```
  on:
    release:
      types: [published]
  ```


#### ```jobs``` Syntax

- ```jobs.<job_id>.name``` 

  - This sets the name of the job. If not specified, GitHub will use the job_is as the name.

  ```
  jobs:
    my_first_job:
      name: My First Job
  ```

- ```jobs.<job_id>.needs``` 

  - This sets the requirements that must be completed before the current job can run. If a required job fails, the current job will not run.

  ```
  jobs:
    my_first_job:
      name: My First Job
    my_second_job:
      name: My Second Job
      needs: my_first_job
  ```

- ```jobs.<job_id>.if``` 

  - Prevent a job from running unless it meets some condition.

  ```
  jobs:
    my_first_job:
      name: My First Job
      if: ${{ ! startsWith(github.ref, 'dev/') }}
  ```

- ```jobs.<job_id>.runs_on``` 

  - Define the type of machine that the job will run on. Can be a single type or an array. Valid types can be [found here](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idruns-on).

  ```
  jobs:
    my_first_job:
      name: My First Job
      runs_on: ubuntu-latest
  ```
![GitHub Logo](images/GitHub_Logo_h33.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Postman Logo](images/Postman-Logo-h33.png)
# GitHub Actions Jobs :: Postman Newman : Sample
## Howto : Setup of a new Postman Newman Testing project
To set up a new Postman Newman Testing project, proceed as follows:

1. Create a new GitHub repository project.

2. Transfer <code>.gitignore</code> and <code>.gitlab-ci.yml</code> from the <code>github-actions-jobs-postman-newman-sample</code>.

3. Configuration of a new GitHub project:

    a. Variables (see in the GitHub project under: <b>Settings</b> => <b>Secrets and Variables</b> => <b>Actions</b>).

4. Make/check the following adjustments in <code>.github/workflows/main.yml</code>:

    a. Configuration of Pipeline name (<code>.name</code>).

      ```yml
      name: Postman Newman - Sample
      ```

    b. Configuration .on.workflow_dispatch.inputs.postmanEnvironment (.options and .default)

      ```yml
      on:
        workflow_dispatch:
          inputs:
            postmanEnvironment:
              description: "Postman Environment"
              required: true
              default: dev
              options:
                - dev
                - qa
              type: choice
      ```
    c. Übergabe von zusätzlichen Postman Environment Variables in <code>.jobs.call-run-postman-newman.secrets.COMMAND_ADDITIONAL_PARAMETERS</code>

      ```yml
      jobs:
        ..
        call-run-postman-newman:
          ..
          secrets:
            ..
            COMMAND_ADDITIONAL_PARAMETERS: "--env-var \"username=${{ secrets.POSTMAN_ENVIRONMENT_USERNAME }}\" --env-var \"password=${{ secrets.POSTMAN_ENVIRONMENT_PASSWORD }}\""
      ```

The following variables and secrets have to be configured (<b>Settings</b> => <b>Secrets and Variables</b> => <b>Actions</b>).

### Variables

#### Environment

Environment specific variables.

<table>
  <tr>
    <th>Variable Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>POSTMAN_ENVIRONMENT_ID</td>
    <td>Postman Environment Id</td>
  </tr>
</table>

#### Repository

<table>
  <tr>
    <th>Variable Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>CUSTOMER_NAME</td>
    <td>Customer Name</td>
  </tr>
  <tr>
    <td>POSTMAN_COLLECTION_ID</td>
    <td>Postman Collection Id</td>
  </tr>
  <tr>
    <td>POSTMAN_TESTING_REPORT_HIDE_REQUEST_BODIES</td>
    <td>If request bodies are not to be included in the report (e.g. because they contain security-relevant information), the variable <code>POSTMAN_TESTING_REPORT_HIDE_REQUEST_BODY</code> must be configured. The Postman request names must be entered in the value of the variable (separated by commas).</td>
  </tr>
  <tr>
    <td>POSTMAN_TESTING_REPORT_HIDE_RESPONSE_BODIES</td>
    <td>If response bodies are not to be included in the report (e.g. because they contain security-relevant information), the variable <code>POSTMAN_TESTING_REPORT_HIDE_RESPONSE_BODY</code> must be configured. The Postman response names must be entered in the value of the variable (separated by commas).</td>
  </tr>
  <tr>
    <td>POSTMAN_TESTING_REPORT_SKIP_ENVIRONMENT_VARS</td>
    <td>If environment variables are not to be included in the report (e.g. because they contain security-relevant information), the variable <code>POSTMAN_TESTING_REPORT_SKIP_ENVIRONMENT_VARS</code> must be configured. The Postman response names must be entered in the value of the variable (separated by commas).</td>
  </tr>
  <tr>
    <td>POSTMAN_TESTING_REPORT_SKIP_HEADERS</td>
    <td>If (request) headers are not to be included in the report (e.g. because they contain security-relevant information), the variable <code>POSTMAN_TESTING_REPORT_SKIP_HEADERS</code> must be configured. The header names must be entered in the value of the variable (separated by commas).</td>
  </tr>      
  <tr>
    <td>POSTMAN_TESTING_REPORT_ITERATION_COUNT</td>
    <td>Iteration count</td>
  </tr>      
</table>

### Secrets

#### Environment

Sometimes, credentials, e.g., for consuming an API, has to be as environment specific secrets.

<table>
  <tr>
    <th>Variable Name</th>
    <th>Mandatory</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>USERNAME</td>
    <td>false</td>
    <td>Sample Username</td>
  </tr>
  <tr>
    <td>PASSWORD</td>
    <td>false</td>
    <td>Sample Password</td>
  </tr>
</table>

#### Repository

<table>
  <tr>
    <th>Variable Name</th>
    <th>Mandatory</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>GHCR_PAT</td>
    <td>true</td>
    <td>GHCR Personal Access Token</td>
  </tr>
  <tr>
    <td>POSTMAN_API_KEY</td>
    <td>true</td>
    <td>Postman API Key</td>
  </tr>
</table>
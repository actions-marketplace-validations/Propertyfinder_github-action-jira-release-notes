# Jira Release Notes
This action generate release notes markdown from Jira project by release version

```markdown
# [Jira](https://your-domain.atlassian.net/projects/project-id/versions/versionJiraId)

### Bug
[NA-1234](https://your-domain.atlassian.net/browse/NA-1234) Ticket summary

### Epic
[NA-1235](https://your-domain.atlassian.net/browse/NA-1235) Ticket summary

### Improvement
[NA-2345](https://your-domain.atlassian.net/browse/NA-2345) Ticket summary
[NA-2346](https://your-domain.atlassian.net/browse/NA-2346) Ticket summary

### Task
[NA-7777](https://your-domain.atlassian.net/browse/NA-7777) Ticket summary
[NA-7780](https://your-domain.atlassian.net/browse/NA-7780) Ticket summary
[NA-7790](https://your-domain.atlassian.net/browse/NA-7790) Ticket summary
```

## Inputs
- `domain`:  `your-domain` value. `https://your-domain.atlassian.net`.
- `project`:  project id. `NA`
- `version`:  version name. ex) `Android 1.0.0`
- `auth-token`:  auth token key.(Not Api key) 

### Auth Token
https://developer.atlassian.com/cloud/jira/platform/basic-auth-for-rest-apis/

1. Generate an API token for Jira using your [Atlassian Account](https://id.atlassian.com/manage/api-tokens).
2. Build a string of the form `useremail:api_token`. (user@example.com:xxxxxxx) 
3. BASE64 encode the string.
- Linux/Unix/MacOS:
```
echo -n user@example.com:api_token_string | base64
```
- Windows 7 and later, using Microsoft Powershell:
```
$Text = ‘user@example.com:api_token_string’
$Bytes = [System.Text.Encoding]::UTF8.GetBytes($Text)
$EncodedText = [Convert]::ToBase64String($Bytes)
$EncodedText
```


## Outputs
- `release_note`: Release notes (Markdown format) 
- `release_notes_url`: Release notes URL(Jira version url) 

## Example usage
```yaml
name: Jira Release Notes
on:
  push:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Jira Release Notes
      id: release_notes
      uses: Propertyfinder/jira-release-note@v1.0
      with:
        domain: 'your-domain'
        project: 'NA'
        version: Android 1.0.0
        auth-token: 'xxxxxxxx'
    - name: Print Release Notes
      run: |
        echo ${{ steps.release_notes.outputs.release_notes }}
```

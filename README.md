# GitHub Docker Action

Build and publish your repository as a Docker image and push it to GitHub Package Registry in one easy step.


## Inputs variables

| With Parameter        | Required/Optional | Description |
| --------------------- | ----------------- | ------------|
| `access_token`        | **Required**     | GitHub Token for the user. Must have write permissions for packages. Recommended set up would be to use the provided GitHub Token for your repository; `${{ secrets.GITHUB_TOKEN }}`.
| `context`             | ***Optional***   | Where should GitHub Docker find the Dockerfile? This is a path relative to the repository root. Defaults to `.`, meaning it will look for a `Dockerfile` in the root of the repository.
| `tags`                | ***Optional***   | The desired name for the image tag. Defaults to current is the commit SHA that triggered the workflow. For example, ffac537e6cbbf934b08745a378932722df287a53.. 
| `image_name`          | ***Optional***   | The desired name for the image. Defaults to current repository name. 
| `build_arg`           | ***Optional***   | Any additional build arguments to use when building the image.
| `username`            | ***Optional***   | GitHub user to publish the image on behalf of. Defaults to the user who triggered the action to run. 
| `repository`          | ***Optional***   | The repository to push the image to. Defaults to current repository. Must be specified in format `user/repo`. Please specify the secret for Personal Access Token [(PAT)](https://help.github.com/es/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line) 

## Outputs variables

| With Parameter        | Required/Optional | Description |
| --------------------- | ----------------- | ------------|
| `imageURL`            | ***Optional***    | The full URL of the image. [See documentation](https://help.github.com/en/actions/reference/workflow-syntax-for-github-actions#jobsjobs_idoutputs)

## Simple usage

```yaml
- name: Publish Image
  uses: craftech-io/github-docker@v1.0.0
  with:
    tags: latest
    access_token: ${{ secrets.GITHUB_TOKEN }}
```

### Use with multiples tags
```yaml
with:
  tags: |
    latest
    anothertag
```
### Use with multiples ARGs
```yaml
with:
  build_args: |
    THISISARG1=test
    THISISARG2=test
```
### Use with outputs variables

```yaml
- name: Publish Image
  uses: craftech-io/github-docker@v1.0.0
  id: url-GPR 
  with:
    tags: latest
    access_token: ${{ secrets.GITHUB_TOKEN }}

- name: output
  run: echo ${{ steps.url-GPR.outputs.imageURL }}    
```

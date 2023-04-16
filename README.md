# Sync up to AWS CodeCommit Action

Synchronize from GitHub repository to AWS CodeCommit via GitHub Actions.  
No need to ssh-private-key. Need to AWS IAM Credentials only.

## Example usage

```yaml
name: GitHub to CodeCommit Sync

on:
  push:
    tags-ignore:
      - '*'
    branches:
      - 'master'

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v1.0.3
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Sync up to CodeCommit
        uses: moinsam/github-to-codecommit-sync@v1.0.1
        with:
          repository_name: test_repo
          aws_region: us-east-1
```

## Inputs

- `repository_name` **Required** CodeCommit repository name.
- `aws_region` **Required** Region of the CodeCommit repository.

## License

[MIT](LICENSE)


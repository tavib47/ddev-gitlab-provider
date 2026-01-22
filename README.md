# DDEV GitLab Provider

A DDEV add-on that provides a pull provider for GitLab Package Registry. Pull database dumps and files uploaded by your CI/CD pipeline directly into your local DDEV environment.

## Installation

```bash
ddev get github.com/tavib47/ddev-gitlab-provider
```

## Configuration

After installation, create `.ddev/.env` with your GitLab credentials:

```bash
# Required
GITLAB_PROJECT_ID=12345678
GITLAB_TOKEN=glpat-xxxxxxxxxxxx

# Optional (defaults shown)
# GITLAB_API_URL=https://gitlab.com/api/v4
# DB_DUMP_PACKAGE_NAME=database
# DB_DUMP_VERSION=test
# FILES_DUMP_PACKAGE_NAME=drupal-files
# FILES_DUMP_VERSION=test
```

### Getting your GitLab Project ID

Find it on your project's main page, under the project name, or in **Settings > General**.

### Creating a GitLab Token

1. Go to https://gitlab.com/-/user_settings/personal_access_tokens
2. Create a token with `read_api` scope
3. Copy the token to your `.ddev/.env` file

## Usage

```bash
# Pull database and files
ddev pull gitlab

# Pull only database
ddev pull gitlab --skip-files

# Pull only files
ddev pull gitlab --skip-db
```

## CI/CD Integration

This provider is designed to work with database and file dumps uploaded to GitLab Package Registry by your CI/CD pipeline.

Expected package structure:
- `database/{version}/dump.sql.gz` - Database dump
- `drupal-files/{version}/public-files.tar.gz` - Public files archive

See [gitlab-ci templates](https://gitlab.com/tavib47/gitlab-ci) for CI/CD templates that upload to the Package Registry.

## Customization

After installation, you can customize the provider by editing `.ddev/providers/gitlab.yaml`.

## Removal

```bash
ddev get --remove ddev-gitlab-provider
```

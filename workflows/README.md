# GitHub Actions Workflows

This directory contains automated workflows for the Brainfile project.

## Workflows

### `ci.yml` - Continuous Integration
**Triggers:** Push to main/develop, Pull Requests

**Purpose:** Ensures code quality and catches issues early

**What it does:**
- Runs tests for both `@brainfile/core` and `@brainfile/cli`
- Builds both packages to verify compilation
- Uploads code coverage reports
- Runs on every push and pull request

**Status Badge:**
```markdown
![CI](https://github.com/YOUR_ORG/brainfile/workflows/CI/badge.svg)
```

### `publish.yml` - NPM Publishing
**Triggers:** 
1. GitHub Releases (automatic)
2. Manual workflow dispatch (manual)

**Purpose:** Publishes packages to npm registry

**What it does:**
- Runs full test suite before publishing
- Builds production artifacts
- Publishes to npm with proper versioning
- Creates git tags for manual publishes
- Publishes `@brainfile/core` first, then `@brainfile/cli`

**Manual Trigger Options:**
- **Package:** Choose `core`, `cli`, or `both`
- **Version:** Choose `patch`, `minor`, or `major`

## Authentication: Trusted Publishing (OIDC) 🔒

**No secrets required!** We use modern OIDC-based trusted publishing.

### Why Trusted Publishing?
- ✅ **No API tokens** - Uses OpenID Connect
- ✅ **No secrets in GitHub** - Authentication handled automatically
- ✅ **Provenance included** - Supply chain transparency
- ✅ **More secure** - Short-lived tokens only
- ✅ **Zero maintenance** - No token rotation needed

### Setup Required:
Configure trusted publishing on npmjs.com for each package:

1. Go to: `https://www.npmjs.com/settings/YOUR_ORG/packages`
2. For each package, add GitHub Actions as trusted publisher
3. Specify:
   - Repository: `YOUR_ORG/brainfile`
   - Workflow: `publish.yml`

📖 **Detailed Guide:** See [TRUSTED_PUBLISHING_SETUP.md](../TRUSTED_PUBLISHING_SETUP.md)

### Legacy: API Token Method (Not Recommended)
<details>
<summary>If you must use tokens (not recommended)</summary>

| Secret Name | Description | How to Get |
|------------|-------------|------------|
| `NPM_TOKEN` | NPM automation token | `npm token create --type=automation` |

⚠️ **Security Risk:** Tokens can leak and require rotation. Use Trusted Publishing instead.
</details>

## Workflow Features

### Dependency Caching
Both workflows use npm cache to speed up builds:
```yaml
- uses: actions/setup-node@v4
  with:
    cache: 'npm'
    cache-dependency-path: core/package-lock.json
```

### Working Directory Support
Each job uses `defaults.run.working-directory` to handle the monorepo structure:
```yaml
defaults:
  run:
    working-directory: ./core
```

### Sequential Publishing
The CLI publish job depends on core:
```yaml
needs: publish-core
```

This ensures `@brainfile/cli` is only published after `@brainfile/core` succeeds.

## Usage Examples

### Automatic Publishing via Release
```bash
# Create and push a tag
git tag -a v0.1.0 -m "Release 0.1.0"
git push origin v0.1.0

# Then create a GitHub release from this tag
# The workflow will automatically publish both packages
```

### Manual Publishing via Workflow Dispatch
1. Go to **Actions** tab in GitHub
2. Select **"Publish to NPM"** workflow
3. Click **"Run workflow"**
4. Select options:
   - Package: `both`
   - Version: `patch`
5. Click **"Run workflow"**

## Monitoring Workflows

### View Workflow Runs
- Go to the **Actions** tab in your repository
- Click on a workflow name to see its runs
- Click on a specific run to see job details and logs

### Workflow Status
- Green checkmark ✓ = Success
- Red X ✗ = Failure
- Yellow circle ○ = In progress

### Debugging Failed Runs
1. Click on the failed workflow run
2. Click on the failed job
3. Expand the failed step
4. Review the error logs
5. Fix the issue and push again

## Best Practices

1. **Always run CI before merging PRs**
   - Ensure all tests pass
   - Verify builds succeed

2. **Use semantic versioning**
   - `patch`: Bug fixes (0.1.0 → 0.1.1)
   - `minor`: New features (0.1.0 → 0.2.0)
   - `major`: Breaking changes (0.1.0 → 1.0.0)

3. **Test locally before publishing**
   ```bash
   ./scripts/check-publish.sh
   ```

4. **Keep secrets secure**
   - Never commit secrets to the repository
   - Rotate tokens periodically
   - Use automation tokens for CI/CD

5. **Review workflow runs**
   - Check logs for warnings
   - Monitor npm publish success
   - Verify published packages

## Troubleshooting

### "permission denied" during publish
- Verify trusted publishing is configured on npmjs.com
- Ensure repository name matches exactly in npm settings
- Check workflow name is correct: `publish.yml`

### "id-token permission not set"
- Workflow should have `permissions.id-token: write`
- Check `.github/workflows/publish.yml` configuration
- This is required for OIDC authentication

### Tests failing in CI but passing locally
- Check Node version consistency
- Verify all dependencies are in package.json
- Look for environment-specific issues
- Try running with `--ci` flag locally

### Build artifacts not found
- Ensure `npm run build` is called before publish
- Check that `dist/` is included in `files` field
- Verify `.npmignore` isn't excluding necessary files

## Extending Workflows

### Adding a New Workflow
1. Create a new `.yml` file in this directory
2. Define triggers and jobs
3. Test with a push or manual trigger
4. Document it in this README

### Adding Workflow Steps
Common steps you might want to add:
- Slack notifications on publish
- Discord webhooks
- GitHub release creation
- Changelog generation
- Smoke tests after publish

## Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [npm Publishing Guide](https://docs.npmjs.com/cli/v9/commands/npm-publish)
- [Workflow Syntax](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions)


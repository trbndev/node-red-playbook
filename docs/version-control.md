# Version Control

## Using GitHub Projects for Git Syncing

1. **Initialize Node-RED project** using the Projects feature
2. **Configure GitHub integration**:
   - Use SSH keys for authentication
   - Set remote origin to your GitHub repository
   - Configure user name and email

3. **Develop using feature branches**:
   - Create branches for new features or fixes
   - Use meaningful branch names (feature/api-integration, fix/validation-error)
   - Commit frequently with descriptive messages

4. **Follow standard Git workflow**:
   - Pull latest changes before starting work
   - Create Pull Requests for review before merging
   - Use GitHub Actions for automated testing if applicable

5. **Manage flow files**:
   - Keep flows organized in logical files
   - Avoid large monolithic flow files
   - Use meaningful file names that describe the flow's purpose

6. **Exclude sensitive data**:
   - Use environment variables or credentials encryption
   - Add sensitive files to .gitignore
   - Never commit credentials or tokens

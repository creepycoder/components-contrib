# DCO Signoff Fix Required

## Issue
The commits in branch `copilot/fix-missing-signoff-commits` are missing the required Developer Certificate of Origin (DCO) signoff as specified in [CONTRIBUTING.md](./CONTRIBUTING.md).

## Affected Commits
1. `2d1bc1e` - "Add enableInOrderMessageDelivery flag to fix session concurrency issue"
   - ❌ Missing `Signed-off-by` line
   
2. `1cf68f8` (or latest) - "Initial plan"  
   - ❌ Missing `Signed-off-by` line

## Required Fix
According to CONTRIBUTING.md section "I didn't sign my commit, now what?!", the fix requires:

```bash
git checkout copilot/fix-missing-signoff-commits
git rebase --root --signoff
git push --force-with-lease origin copilot/fix-missing-signoff-commits
```

## Why This Wasn't Done Automatically
The automated agent environment has security restrictions that prevent force pushing to remote branches. This is intentional to protect repository history. The fix requires manual intervention from a user with appropriate repository permissions.

## Manual Fix Steps
A repository maintainer or user with push access should:

1. **Clone the repository and checkout the branch:**
   ```bash
   git clone https://github.com/creepycoder/components-contrib
   cd components-contrib
   git checkout copilot/fix-missing-signoff-commits
   ```

2. **Add signoff to all commits:**
   ```bash
   git rebase --root --signoff
   ```

3. **Verify the signoff was added:**
   ```bash
   git log --format="%H%n%B%n---" -3
   ```
   Each commit should end with a line like:
   ```
   Signed-off-by: Your Name <your.email@example.com>
   ```

4. **Force push the signed commits:**
   ```bash
   git push --force-with-lease origin copilot/fix-missing-signoff-commits
   ```

## After Fix
Once the force push is complete:
- All commits will have the required DCO signoff
- The DCO bot check should pass
- This instruction file can be removed
- The pull request can proceed with review

## Reference
- [Developer Certificate of Origin](https://developercertificate.org/)
- [Project CONTRIBUTING.md](./CONTRIBUTING.md#developer-certificate-of-origin-signing-your-work)

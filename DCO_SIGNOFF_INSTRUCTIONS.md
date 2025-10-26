# DCO Signoff Fix Required

## Issue
The commits in branch `copilot/fix-missing-signoff-commits` are missing the required Developer Certificate of Origin (DCO) signoff as specified in [CONTRIBUTING.md](./CONTRIBUTING.md).

## Current Branch State
The branch currently has duplicate commits due to multiple automated fix attempts:
- `df46893` - "Add DCO signoff fix instructions" - ✅ Has signoff (this document)
- `410be15`, `d925eb7`, `1cf68f8` - Duplicate "Initial plan" commits (from failed fix attempts)
- `2d1bc1e` - "Add enableInOrderMessageDelivery flag to fix session concurrency issue" - ❌ Missing signoff

## Root Cause
The original commits that need signoff:
1. `2d1bc1e` - "Add enableInOrderMessageDelivery flag to fix session concurrency issue"
2. The first "Initial plan" commit

Attempts to automatically rebase and add signoff created duplicates because force push is restricted in the automated environment.

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

2. **Reset to the base commit (before duplicates):**
   ```bash
   git reset --hard 2d1bc1e
   ```

3. **Amend the first commit with signoff:**
   ```bash
   git commit --amend --no-edit --signoff
   ```

4. **Recreate the "Initial plan" commit with signoff:**
   ```bash
   git commit --allow-empty -m "Initial plan" --signoff
   ```

5. **Verify both commits have signoff:**
   ```bash
   git log --format="%h %s%n%b" -2
   ```
   Each commit should end with:
   ```
   Signed-off-by: copilot-swe-agent[bot] <198982749+Copilot@users.noreply.github.com>
   ```

6. **Force push the clean, signed commits:**
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

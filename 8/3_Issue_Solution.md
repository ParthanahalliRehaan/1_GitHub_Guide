## ⚠️ The Issue
- You had **multiple `user.name` and `user.email` values** stored in your Git config.  
- Commits were showing with the wrong author name (`RehaanParthanahlli`) and the wrong email (`parthanahallirehaan@gmail.com`).  
- GitHub only counts contributions if the commit email matches a **verified email** in your account.  
- Because of the mismatch, your contributions graph stayed empty for months.

---

## ✅ The Solution
1. **Check commit metadata**  
   ```bash
   git log --pretty=format:"%h %an %ae" -5
   ```
   Shows last 5 commits with author name + email.  
   → This revealed the wrong name/email being used.

2. **Check stored config values**  
   ```bash
   git config --global --get-all user.name
   git config --global --get-all user.email
   ```
   → Showed duplicates.

3. **Clean up duplicates**  
   ```bash
   git config --global --unset-all user.name
   git config --global --unset-all user.email
   ```

4. **Set correct global identity (default)**  
   ```bash
   git config --global user.name "ParthanahalliRehaan"
   git config --global user.email "parthanahalli.rehaan@gmail.com"
   ```

5. **Set per‑repo identity (for multiple accounts)**  
   Inside each repo:
   ```bash
   git config user.name "ParthanahalliRehaan"
   git config user.email "parthanahallirehaan@gmail.com"
   ```
   → This ensures each repo commits with the right account identity.

6. **Verify emails in GitHub**  
   - Add and verify both `parthanahalli.rehaan@gmail.com` and `parthanahallirehaan@gmail.com` in your GitHub account.  
   - GitHub treats them as different strings (dot matters here), so both must be verified.

---

## 🧭 Key Commands Recap
```bash
# Check commit author info
git log --pretty=format:"%h %an %ae" -5

# Check stored config values
git config --global --get-all user.name
git config --global --get-all user.email

# Remove duplicates
git config --global --unset-all user.name
git config --global --unset-all user.email

# Set correct global identity
git config --global user.name "ParthanahalliRehaan"
git config --global user.email "parthanahalli.rehaan@gmail.com"

# Set per-repo identity (inside repo folder)
git config user.name "ParthanahalliRehaan"
git config user.email "parthanahallirehaan@gmail.com"
```

---

⚡ **Lesson learned the hard way**: Always set `user.name` and `user.email` per repo when using multiple GitHub accounts, and make sure every commit email is verified in GitHub. That way, you’ll never lose contributions again.  

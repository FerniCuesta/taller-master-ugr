# taller-master-ugr
A repository to showcase how GitHub works to master students

# Intermediate Level Exercise

Welcome to the Intermediate level! This exercise will teach you about merging branches, resolving conflicts, and using tags.

## Exercise - Merging, Conflict Resolution, and Tagging
**Objective**: Learn to merge branches, handle merge conflicts effectively, and create tags for version control.

**Tasks**:

### Part 1: Merging Branches and Resolving Conflicts
1. Create two branches from intermediate:
   ```bash
   git checkout intermediate
   git checkout -b feature/header
   git checkout intermediate
   git checkout -b feature/footer
   ```

2. In `feature/header` branch:
   * Create a file `page.html` with a header section
   * Commit your changes:
   ```bash
   git add page.html
   git commit -m "Add header to page"
   ```

3. Switch to `feature/footer` branch:
   ```bash
   git checkout feature/footer
   ```
   * Create the same file `page.html` but with a footer section
   * Commit your changes:
   ```bash
   git add page.html
   git commit -m "Add footer to page"
   ```

4. Merge both branches into intermediate:
   ```bash
   git checkout intermediate
   git merge feature/header
   git merge feature/footer  # This will create a conflict!
   ```

5. Resolve the conflict:
   * Open `page.html` and manually merge the changes
   * Keep both header and footer sections
   * Stage the resolved file: `git add page.html`
   * Complete the merge: `git commit -m "Merge footer with resolved conflicts"`

### Part 2: Using Tags
1. Create an annotated tag for your current work:
   ```bash
   git tag -a v1.0 -m "First stable version with merged features"
   ```

2. List all tags:
   ```bash
   git tag
   ```

3. View tag information:
   ```bash
   git show v1.0
   ```

4. Push the tag to remote:
   ```bash
   git push origin v1.0
   ```

5. Create a lightweight tag for testing:
   ```bash
   git tag v1.0-test
   ```

6. Compare the two types of tags:
   ```bash
   git show v1.0
   git show v1.0-test
   ```

**Success Criteria**:
- You can successfully merge branches without conflicts
- You can identify and resolve merge conflicts
- You understand the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
- You can create and push both annotated and lightweight tags
- You understand the difference between tag types and when to use each

---

## 📤 Submitting Your Work

### Congratulations on completing the Intermediate Level! 🎉

You've mastered merging, conflict resolution, and tagging. Time to document your achievements!

### Step 1: Create Your Outcome Branch

From the intermediate branch, create your group's outcome branch:

```bash
git checkout intermediate
git checkout -b group-X-outcomes/intermediate
```

### Step 2: Document Your Outcomes

1. **Get the template**:
   ```bash
   git checkout main -- OUTCOME_TEMPLATE.md
   cp OUTCOME_TEMPLATE.md OUTCOMES.md
   ```

2. **Complete `OUTCOMES.md`** with:
   
   **Part 1 - Merging & Conflicts**:
   - Commands used to create branches and make conflicting changes
   - Output from `git merge` showing the conflict
   - The conflict markers you saw in your file
   - How you resolved the conflict
   - `git log --graph --oneline --all` showing merge commit
   
   **Part 2 - Tags**:
   - Commands for creating annotated and lightweight tags
   - Output from `git tag` and `git show v1.0`
   - Comparison between annotated and lightweight tags
   - Explanation of when to use each type of tag

3. **Document your challenges**:
   - How did you approach your first merge conflict?
   - Any difficulties understanding conflict markers?
   - Confusion about when to use annotated vs. lightweight tags?
   - What resources did you use to solve problems?

4. **Reflect deeply**:
   - How does merge conflict resolution work?
   - When would you use tags in a real project?
   - What's the difference between tags and branches?
   - How do tags help with versioning and releases?

### Step 3: Commit Your Documentation

```bash
git add OUTCOMES.md
git commit -m "docs: Add intermediate level exercise outcomes for Group X"
```

### Step 4: Push to Remote

```bash
git push origin group-X-outcomes/intermediate
```

### Step 5: Create Pull Request (If Required)

Submit a PR with title: "Outcomes: Group X - Intermediate Level"

### What to Include

✅ **Part 1 Requirements**:
- At least 2 branches with conflicting changes
- Screenshot or output showing conflict markers
- Resolution strategy explained
- Merge commit in git log
- `git log --graph` showing branch structure

✅ **Part 2 Requirements**:
- At least 1 annotated tag and 1 lightweight tag created
- Tag information with `git show` for both types
- Comparison explaining the differences
- When to use each type of tag

✅ **General Requirements**:
- Complete command history with outputs
- Screenshots of complex operations (optional)
- Detailed problem-solving narratives
- Reflection (minimum 150 words)
- Self-assessment for all intermediate topics

### Evaluation Criteria

| Criterion | Weight | Key Focus for Intermediate Level |
|-----------|--------|----------------------------------|
| Completion | 20% | Exercise completed with all parts and full documentation |
| Understanding | 25% | Merge strategies, conflict resolution, and tag concepts |
| Practical Skills | 25% | Clean conflict resolution and proper tag usage |
| Problem-Solving | 20% | How you debugged conflicts and resolved issues |
| Documentation | 10% | Clear explanations of complex operations |

**Minimum score to advance to Master level**: 75/100

### Common Challenges to Document

💡 **Merge Conflicts**:
- How did you identify which changes to keep?
- Did you accidentally break code during resolution?
- How did you verify the merge was correct?

💡 **Tags vs. Branches**:
- Can you explain when to use each?
- Did you try pushing tags? What happened?

💡 **Tag Types**:
- What's the difference between annotated and lightweight tags?
- When should you use each type?
- How do you push tags to remote?

### Tips for Success

📝 Document conflicts BEFORE resolving them (screenshot!)  
📝 Save git log output at key points  
📝 Explain your thought process, not just commands  
📝 Connect concepts to real-world scenarios  
📝 Show both successes and mistakes  

### Resources

- Merge conflicts: https://git-scm.com/docs/git-merge
- Tags: https://git-scm.com/book/en/v2/Git-Basics-Tagging
- Conflict resolution: https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging

---

**Next Steps**: Once you've mastered these skills, move to the `master` branch for advanced Git techniques including rewriting history with rebase and amend!


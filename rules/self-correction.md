# Self-Correction Process

## Principle

Failure is expected. The response to failure matters.

## The Rule

**3 consecutive failures on the same issue → Stop and escalate**

## Process

```
Attempt 1 → Failure
    ↓
Analyze error → Identify cause → Fix → Retry

Attempt 2 → Failure
    ↓
Analyze differently → Try different approach → Retry

Attempt 3 → Failure
    ↓
┌─────────────────────────────────────┐
│ STOP - REVERT - DOCUMENT - ASK     │
└─────────────────────────────────────┘
```

## Step-by-Step

### On Failure 1-2

1. **Read the error message carefully**
   - Don't skim, read fully
   - Note the specific line/file

2. **Analyze the cause**
   - Is it a typo?
   - Wrong assumption?
   - Missing dependency?

3. **Fix and retry**
   - Make targeted fix
   - Don't change unrelated code
   - Verify the fix

### On Failure 3

1. **STOP**
   - Do not attempt another fix
   - Do not try "one more thing"

2. **REVERT**
   ```bash
   git checkout -- [affected files]
   # or
   git stash
   ```
   - Return to last known working state
   - Don't leave broken code

3. **DOCUMENT**
   ```markdown
   ## Failed Attempts

   ### Attempt 1
   - Action: [what I tried]
   - Error: [what happened]
   - Analysis: [why I thought it failed]

   ### Attempt 2
   - Action: [different approach]
   - Error: [what happened]
   - Analysis: [updated understanding]

   ### Attempt 3
   - Action: [another approach]
   - Error: [what happened]
   - Analysis: [why all approaches failed]
   ```

4. **ANALYZE**
   - What's the common thread?
   - What assumption might be wrong?
   - What information am I missing?

5. **ASK**
   ```markdown
   I've attempted to [goal] 3 times without success.

   ## What I tried
   [summary of attempts]

   ## What I observed
   [errors and behaviors]

   ## My analysis
   [what I think is happening]

   ## Questions
   - [specific question 1]
   - [specific question 2]

   How would you like me to proceed?
   ```

## What Counts as "Same Issue"

**Same issue:**
- Build fails with same error
- Same test keeps failing
- Same type of bug reappears

**Different issue:**
- New error after fixing previous
- Different test failing
- Progressed but hit new problem

**Reset counter when:**
- Successfully resolved an issue
- User provides new information
- Switching to different task

## Examples

### Good: Proper Escalation

```
Attempt 1: Added missing import → Still fails (different error)
Attempt 2: Fixed typo in function name → Still fails (same error)
Attempt 3: Tried alternative approach → Still fails (same error)

"I've tried 3 approaches to fix this build error without success.
All attempts result in the same 'Module not found' error.
I've reverted to the working state. Could you check if there's
a configuration issue I might be missing?"
```

### Bad: Endless Loop

```
Attempt 1: Changed X → Failed
Attempt 2: Changed Y → Failed
Attempt 3: Changed Z → Failed
Attempt 4: Changed X again → Failed
Attempt 5: Combined X and Y → Failed
... (continues indefinitely)
```

## Why This Matters

1. **Prevents wasted effort** - Repeating failed approaches
2. **Preserves working code** - Revert before more damage
3. **Enables help** - User can provide missing context
4. **Maintains trust** - Transparent about limitations

## Integration with Workflow

```
[Implementation Loop]
     ↓
   Failure → Count < 3? → Analyze → Fix → Retry
     ↓           ↓
   Count = 3     Yes
     ↓
   STOP → REVERT → DOCUMENT → ASK
```

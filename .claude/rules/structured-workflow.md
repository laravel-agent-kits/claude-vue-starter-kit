# Structured Workflow Guidelines

## 🚨 MANDATORY: Four-Phase Development Workflow

**This project enforces a strict four-phase workflow.** You MUST NOT write implementation code until explicitly authorized by the user. Every task follows the **Explore → Plan → Validate → Implement** cycle.

---

## The Four Phases

```
┌─────────────────────────────────────────────────────────────────┐
│  PHASE 1: EXPLORE   →   PHASE 2: PLAN   →   PHASE 3: VALIDATE  │
│       (Gather)            (Propose)           (Confirm)         │
│                                                                 │
│                              ↓                                  │
│                                                                 │
│                     PHASE 4: IMPLEMENT                          │
│                        (Execute)                                │
└─────────────────────────────────────────────────────────────────┘
```

**⛔ CODE WRITING IS FORBIDDEN IN PHASES 1-3**

---

## Phase 1: EXPLORE (Discovery Mode)

### Purpose
Gather complete context before making any decisions. Understand the codebase, existing patterns, and constraints.

### Required Actions

1. **Acknowledge the request** and enter exploration mode
2. **Ask the user which files/areas to explore:**
   ```
   "Before I plan anything, I need to understand the current codebase. 
   Which files or directories should I explore? For example:
   - Existing related components/services?
   - Database migrations or models?
   - Configuration files?
   - Test files?"
   ```

3. **Read and analyze the specified files** using appropriate tools
4. **Document your findings** - summarize what you learned:
    - Existing patterns and conventions
    - Related code that will be affected
    - Potential constraints or dependencies
    - Technical debt or issues to consider

### Phase 1 Output Template
```markdown
## 📂 Exploration Summary

### Files Reviewed
- `path/to/file1.php` - [brief description of what it does]
- `path/to/file2.php` - [brief description of what it does]

### Existing Patterns Observed
- [Pattern 1]
- [Pattern 2]

### Dependencies & Constraints
- [Dependency/Constraint 1]
- [Dependency/Constraint 2]

### Questions or Concerns
- [Any clarifications needed]

---
Ready to proceed to planning? Or should I explore additional files?
```

### ❌ Forbidden in Phase 1
- Writing any implementation code
- Creating files
- Making changes to existing files
- Proposing detailed solutions

---

## Phase 2: PLAN (Architecture Mode)

### Purpose
Design a comprehensive implementation plan based on exploration findings. Present a clear roadmap for the user to review.

### Required Actions

1. **Announce entry into planning phase:**
   ```
   "Based on my exploration, I'll now formulate a detailed implementation plan."
   ```

2. **Create a structured plan** including:
    - Overview of the approach
    - Step-by-step implementation tasks
    - Files to be created/modified
    - Subagent delegation assignments
    - Potential risks and mitigations
    - Testing strategy

### Phase 2 Output Template
```markdown
## 📋 Implementation Plan

### Overview
[High-level description of what will be built and the approach]

### Implementation Steps

#### Step 1: [Task Name]
- **Subagent:** `[agent-name]`
- **Files affected:** `path/to/file.php`
- **Description:** [What will be done]
- **Acceptance criteria:** [How we know it's done]

#### Step 2: [Task Name]
- **Subagent:** `[agent-name]`
- **Files affected:** `path/to/file.php`
- **Description:** [What will be done]
- **Acceptance criteria:** [How we know it's done]

[Continue for all steps...]

### Files to Create
| File Path | Purpose |
|-----------|---------|
| `app/Services/NewService.php` | [Purpose] |
| `resources/js/pages/NewPage.vue` | [Purpose] |

### Files to Modify
| File Path | Changes |
|-----------|---------|
| `routes/api.php` | Add new endpoint |
| `app/Models/User.php` | Add relationship |

### Risk Assessment
| Risk | Likelihood | Mitigation |
|------|------------|------------|
| [Risk 1] | Low/Med/High | [How to handle] |

### Testing Strategy
- [ ] Unit tests for [component]
- [ ] Feature tests for [feature]
- [ ] Manual testing checklist

---
**Please review this plan.** Reply with:
- ✅ "Approved" or "Proceed" to begin implementation
- 🔄 "Revise [specific part]" for changes
- ❓ Questions for clarification
```

### ❌ Forbidden in Phase 2
- Writing any implementation code
- Creating files
- Making changes to existing files
- Beginning work without explicit approval

---

## Phase 3: VALIDATE (Confirmation Gate)

### Purpose
Ensure the user has reviewed and explicitly approved the plan before any implementation begins.

### Required Actions

1. **Wait for explicit user approval** - Do not proceed without one of these signals:
    - "Approved"
    - "Proceed"
    - "Go ahead"
    - "Looks good"
    - "Start implementation"
    - "Execute"
    - Or similar clear confirmation

2. **Handle revision requests:**
    - If user requests changes, return to Phase 2
    - Update the plan based on feedback
    - Re-present for validation

3. **Handle questions:**
    - Answer any clarifying questions
    - Remain in Phase 3 until approved

### Validation Checkpoints
```markdown
## ✅ Pre-Implementation Checklist

Before proceeding, confirm:
- [ ] User has explicitly approved the plan
- [ ] All questions have been answered
- [ ] Scope is clearly defined
- [ ] File changes are documented
- [ ] Subagent assignments are clear

User approval received: [YES/NO]
```

### ❌ Forbidden in Phase 3
- Starting implementation without explicit approval
- Assuming silence means approval
- Interpreting ambiguous responses as approval

---

## Phase 4: IMPLEMENT (Execution Mode)

### Purpose
Execute the approved plan by delegating to appropriate subagents.

### Required Actions

1. **Announce entry into implementation phase:**
   ```
   "Plan approved! Beginning implementation..."
   ```

2. **Follow the plan exactly** - Implement in the order specified

3. **Delegate to subagents** as outlined in the plan:
    - Use `Task` tool for each delegation
    - Provide context from exploration phase
    - Reference the approved plan

4. **Report progress** after each step:
   ```
   "✅ Step 1 complete: [description]
    → Proceeding to Step 2..."
   ```

5. **Provide completion summary:**
   ```markdown
   ## ✅ Implementation Complete

   ### Completed Steps
   - [x] Step 1: [description]
   - [x] Step 2: [description]
   
   ### Files Created
   - `path/to/new/file.php`
   
   ### Files Modified
   - `path/to/modified/file.php`
   
   ### Testing
   - [ ] Run: `php artisan test --filter=NewFeatureTest`
   
   ### Next Steps (if any)
   - [Recommendation 1]
   - [Recommendation 2]
   ```

---

## Workflow Triggers

### Entering Plan Mode
User can explicitly request planning with phrases like:
- "Let's plan this out"
- "Enter plan mode"
- "I need to implement [feature]"
- "Help me build [feature]"
- "Can you create [feature]"

### Implicit Plan Mode
ANY request that involves:
- Creating new features
- Modifying existing functionality
- Refactoring code
- Bug fixes (non-trivial)
- Performance improvements

**Should automatically trigger the four-phase workflow.**

---

## Quick Reference Commands

| User Says | Your Action |
|-----------|-------------|
| "Plan mode" / "Let's plan" | Start Phase 1 (Explore) |
| "Explore [files]" | Continue Phase 1 with specified files |
| "I've told you enough, plan it" | Move to Phase 2 (Plan) |
| "Approved" / "Proceed" / "Go ahead" | Move to Phase 4 (Implement) |
| "Revise..." / "Change..." | Return to Phase 2 |
| "Stop" / "Cancel" | Exit workflow |
| "Skip to implementation" | ⚠️ Confirm they understand risks, then proceed |

---

## Example Workflow

### User Request
```
"I need to add a feature where users can export their data as CSV"
```

### Phase 1: EXPLORE
```
"I'll help you implement CSV data export. Before I create a plan, I need to explore the codebase.

Which files should I review? I'm thinking:
- User model and related models (to understand data structure)
- Existing export functionality (if any)
- Current controllers handling user data
- Any existing report/download features

Please confirm or suggest specific files to explore."
```

*[User specifies files]*

*[You read and analyze files]*

```
## 📂 Exploration Summary

### Files Reviewed
- `app/Models/User.php` - User model with profile, orders, activities relationships
- `app/Http/Controllers/AccountController.php` - Handles account settings
- `app/Exports/` - Directory doesn't exist, no current export functionality

### Existing Patterns Observed
- Controllers use Form Requests for validation
- Jobs are used for heavy processing
- Notifications are sent for completed actions

### Dependencies & Constraints  
- Users can have large datasets (10k+ orders)
- Need to consider memory limits for large exports

Ready to proceed to planning?
```

### Phase 2: PLAN
```
## 📋 Implementation Plan

### Overview
Implement CSV export allowing users to download their personal data. Will use queued jobs for large exports and direct download for small datasets.

### Implementation Steps

#### Step 1: Create Export Service
- **Subagent:** `backend-engineer`
- **Files:** `app/Services/UserDataExportService.php`
- **Description:** Service to collect and format user data for export

#### Step 2: Create Export Job
- **Subagent:** `backend-engineer`  
- **Files:** `app/Jobs/ProcessUserDataExport.php`
- **Description:** Queued job for large exports

#### Step 3: Create API Endpoint
- **Subagent:** `backend-engineer`
- **Files:** `app/Http/Controllers/Api/ExportController.php`, `routes/api.php`
- **Description:** Endpoint to trigger and download exports

#### Step 4: Create UI Component
- **Subagent:** `ui-engineer`
- **Files:** `resources/js/components/ExportDataButton.vue`
- **Description:** Vue component with progress indicator

[...]

Please review this plan and reply "Approved" to proceed.
```

### Phase 3: VALIDATE
*[User reviews and responds]*

```
User: "Looks good, but can we also add PDF export option?"
```

```
"I'll revise the plan to include PDF export..."

[Returns to Phase 2 with updated plan]
```

```
User: "Approved"
```

### Phase 4: IMPLEMENT
```
"Plan approved! Beginning implementation...

Starting Step 1: Creating Export Service
→ Delegating to backend-engineer..."

[Task tool delegation]

"✅ Step 1 complete: Export service created

Proceeding to Step 2: Creating Export Job..."

[Continues through all steps]
```

---

## Anti-Patterns (DO NOT DO)

❌ **Never skip exploration:**
```
User: "Add a payment feature"
You: "Here's the plan..." // Wrong! Ask what to explore first
```

❌ **Never assume approval:**
```
You: "Here's my plan... I'll start implementing now." // Wrong! Wait for explicit approval
```

❌ **Never write code during planning:**
```
You: "In step 1, we'll create this service:
```php
class MyService { // Wrong! No code until Phase 4
```
```

❌ **Never deviate from approved plan without re-validation:**
```
You: "I noticed we also need X, so I added it..." // Wrong! Get approval for changes
```

---

## Enforcement Checklist

Before ANY code is written, verify:

- [ ] **Phase 1 Complete:** Files explored, patterns documented
- [ ] **Phase 2 Complete:** Detailed plan presented
- [ ] **Phase 3 Complete:** Explicit user approval received
- [ ] **Phase 4 Entry:** Approval confirmed, ready to delegate

**If any checkbox is unchecked, STOP and complete the missing phase.**

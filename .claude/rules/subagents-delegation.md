# Subagent Delegation Guidelines

## MANDATORY: Always Use Subagents for Task Execution

**This project enforces strict subagent delegation.** You MUST NOT directly implement features, fix bugs, or make code changes yourself. Instead, you MUST delegate all implementation work to the appropriate specialized subagent using the `Task` tool.

---

## Core Principle

**Your role as the orchestrator is to:**
1. Understand the user's request
2. Break down complex tasks into subtasks if needed
3. Identify the correct subagent(s) for each task
4. Delegate using the `Task` tool
5. Coordinate results and report back to the user

**You are NOT permitted to:**
- Write implementation code directly
- Make changes to files without delegating to a subagent
- Skip subagent delegation for "simple" tasks

---

## Available Subagents

### 1. `backend-engineer`

**Use for ALL backend-related work including:**
- API endpoints (REST, GraphQL)
- Database schemas, migrations, seeders
- Eloquent models, relationships, scopes
- Service classes, repositories, actions
- Queue jobs, scheduled tasks, workers
- Authentication & authorization (policies, gates, middleware)
- Payment processing, subscription logic
- Query optimization, N+1 fixes, indexing
- Caching strategies (Redis, file, database)
- Third-party API integrations
- Validation rules and form requests
- Event/listener implementations
- Console commands (Artisan)
- Backend testing (Feature tests, Unit tests)
- Inertia controller responses and props

**Trigger keywords:** API, endpoint, database, model, migration, query, service, repository, authentication, authorization, policy, gate, middleware, queue, job, cache, validation, Eloquent, controller, route, artisan, scheduler, event, listener, Inertia response

---

### 2. `ui-engineer`

**Use for ALL frontend and UI work including:**
- Vue 3 single-file components
- Inertia.js page components
- TypeScript interfaces and types
- Vue composables
- shadcn-vue component implementation
- Form components with validation UX
- Data tables, lists, grids
- Modals, dropdowns, navigation
- Real-time updates and polling
- File uploads, drag-and-drop
- Component state management
- Frontend validation feedback
- Toast notifications, alerts
- Loading states, skeleton screens
- Tailwind CSS styling and responsive design
- Dark mode implementation
- Visual hierarchy and spacing
- Accessibility compliance (WCAG)
- Animation and transitions
- Mobile-first design patterns
- Component visual polish and refinement

**Trigger keywords:** component, Vue, Inertia, page, template, form, modal, dropdown, navigation, view, frontend, UI, interactive, real-time, Tailwind, styling, responsive, mobile, design, visual, colors, spacing, accessibility, WCAG, a11y, animation, TypeScript, composable, shadcn

---

### 3. `qa-expert`

**Use for ALL quality assurance and testing work including:**
- Test strategy and planning
- Manual testing (exploratory, usability, accessibility)
- Test automation framework setup
- End-to-end (E2E) browser testing with Playwright
- API testing and contract validation
- Performance and load testing
- Security testing and vulnerability assessment
- Test case design and documentation
- Defect tracking and root cause analysis
- Regression test suite management
- CI/CD test integration
- Quality metrics and reporting
- User acceptance testing (UAT) coordination
- Test data management
- Cross-browser and device compatibility testing
- Vue component testing with Vitest
- Inertia response testing
- Visual verification and screenshot comparison

**Trigger keywords:** test, testing, QA, quality, bug, defect, regression, E2E, end-to-end, Playwright, automation, coverage, performance test, load test, security test, UAT, acceptance, smoke test, test case, test plan, quality assurance, verify, validate, Vitest

**Special Capabilities:**
- Has access to Playwright MCP tools for browser automation
- Has access to Laravel Boost MCP tools for application introspection
- Can execute database queries for test data verification
- Can take screenshots and analyze UI states
- Can monitor network requests and console logs

---

## Decision Matrix

| Task Type | Primary Subagent | Secondary (if needed) |
|-----------|------------------|----------------------|
| New API endpoint | `backend-engineer` | `qa-expert` (for tests) |
| New Inertia page with form | `ui-engineer` | `backend-engineer` (controller) |
| Database optimization | `backend-engineer` | - |
| Vue component styling issues | `ui-engineer` | - |
| Full feature (end-to-end) | `backend-engineer` → `ui-engineer` → `qa-expert` | - |
| Accessibility fixes | `ui-engineer` | `qa-expert` (for verification) |
| Vue component logic | `ui-engineer` | `backend-engineer` (if API needed) |
| Authentication system | `backend-engineer` | `qa-expert` (security testing) |
| Design system setup | `ui-engineer` | - |
| Bug investigation | `qa-expert` | Relevant implementation agent |
| E2E test automation | `qa-expert` | - |
| Performance issues (backend) | `backend-engineer` | `qa-expert` (load testing) |
| Performance issues (frontend) | `ui-engineer` | `qa-expert` (verification) |
| API testing | `qa-expert` | `backend-engineer` |
| Pre-release validation | `qa-expert` | - |
| Test coverage gaps | `qa-expert` | - |
| Security audit | `qa-expert` | `backend-engineer` |
| Responsive design | `ui-engineer` | `qa-expert` (cross-device testing) |
| Visual polish/refinement | `ui-engineer` | - |
| Dark mode implementation | `ui-engineer` | `qa-expert` (verification) |
| TypeScript types/interfaces | `ui-engineer` | - |
| Composable creation | `ui-engineer` | - |

---

## Delegation Protocol

### Step 1: Analyze the Request
Before responding, categorize the task:
- Is this backend logic, API, or database? → `backend-engineer`
- Is this a Vue component, styling, or visual? → `ui-engineer`
- Is this testing, QA, or bug investigation? → `qa-expert`
- Is this mixed? → Plan multi-agent workflow

### Step 2: Announce Your Delegation
Always tell the user which agent you're delegating to and why:
```
"This task involves [description]. I'll delegate this to the `[agent-name]` agent to ensure [reason]."
```

### Step 3: Use the Task Tool
Delegate with clear, specific instructions:
```
Task(agent: "[agent-name]", prompt: "[Detailed task description with context]")
```

### Step 4: Coordinate Multi-Agent Tasks
For complex features requiring multiple agents:

1. **Backend First:** Delegate data layer, API, and Inertia controllers to `backend-engineer`
2. **UI Second:** Delegate Vue component implementation and styling to `ui-engineer`
3. **QA Last:** Delegate testing and validation to `qa-expert`

---

## Examples of Proper Delegation

### Example 1: Simple API Endpoint
```
User: "Add an endpoint to fetch user notifications"

You: "This requires backend API implementation. I'll delegate to the backend-engineer agent."

→ Task(agent: "backend-engineer", prompt: "Create a GET endpoint at /api/notifications to fetch the authenticated user's notifications. Include pagination, filtering by read/unread status, and proper API Resource transformation.")
```

### Example 2: New Dashboard Component
```
User: "Create a stats widget showing monthly revenue"

You: "This needs a Vue component with data visualization. I'll delegate to the ui-engineer agent."

→ Task(agent: "ui-engineer", prompt: "Create a Vue 3 component for displaying monthly revenue statistics. Use `<script setup>` with TypeScript, include a chart visualization using appropriate shadcn-vue components, comparison with previous month, loading states, and responsive design for mobile.")
```

### Example 3: New Inertia Page
```
User: "Create a user profile settings page"

You: "This requires both backend (Inertia controller) and frontend (Vue page). I'll coordinate between backend-engineer and ui-engineer."

→ Task(agent: "backend-engineer", prompt: "Create a ProfileController with edit and update methods. Return Inertia responses with proper props for the profile form. Include form validation with a ProfileUpdateRequest.")

→ Task(agent: "ui-engineer", prompt: "Create a Vue page component at resources/js/pages/settings/Profile.vue. Use `<script setup>` with TypeScript, Inertia's useForm for form handling, shadcn-vue form components, proper validation error display, and loading states.")
```

### Example 4: Component Styling and Visual Polish
```
User: "The product card looks outdated and needs better styling"

You: "This requires UI refinement and visual improvements. I'll delegate to the ui-engineer agent."

→ Task(agent: "ui-engineer", prompt: "Refactor the product card Vue component to improve visual design. Update Tailwind CSS styling for better visual hierarchy, spacing, and modern aesthetics. Ensure responsive design, dark mode support, and accessibility compliance.")
```

### Example 5: Write E2E Tests for Checkout Flow
```
User: "We need automated tests for the checkout process"

You: "This requires end-to-end test automation. I'll delegate to the qa-expert agent."

→ Task(agent: "qa-expert", prompt: "Create comprehensive E2E tests for the checkout flow using Playwright. Cover: adding items to cart, applying discounts, entering shipping info, payment processing, order confirmation. Include happy path and error scenarios.")
```

### Example 6: Investigate and Fix a Bug
```
User: "Users are reporting that the order total sometimes shows wrong"

You: "This needs investigation first. I'll delegate to the qa-expert agent to identify the root cause."

→ Task(agent: "qa-expert", prompt: "Investigate the order total calculation bug. Reproduce the issue, identify edge cases, and document the root cause with steps to reproduce.")

[After QA identifies the issue]

You: "The qa-expert has identified the issue is in the discount calculation service. I'll delegate the fix to backend-engineer."

→ Task(agent: "backend-engineer", prompt: "Fix the discount calculation bug in OrderTotalService. Issue: [details from QA]. Ensure the fix handles [edge cases identified].")

→ Task(agent: "qa-expert", prompt: "Verify the fix for the order total calculation bug. Run regression tests and confirm all identified edge cases are now handled correctly.")
```

### Example 7: Full Feature Implementation with QA
```
User: "Build a user profile page where users can update their info"

You: "This is a full-stack feature. I'll coordinate between multiple agents:
1. First, backend-engineer for the Inertia controller and validation
2. Then, ui-engineer for the Vue page component and visual design
3. Finally, qa-expert for comprehensive testing"

→ Task(agent: "backend-engineer", prompt: "Create profile update functionality: ProfileController with edit/update methods, ProfileUpdateRequest form request validation, profile photo upload handling with storage, and proper Inertia responses with user data...")

→ Task(agent: "ui-engineer", prompt: "Create a profile edit Vue page using `<script setup>` with TypeScript. Use Inertia's useForm for form handling, shadcn-vue form fields for name, email, bio, and avatar upload. Include proper validation feedback, loading states, success notifications, responsive design, and visual polish...")

→ Task(agent: "qa-expert", prompt: "Create comprehensive test coverage for the profile feature: unit tests for validation, feature tests for Inertia responses, Vue component tests with Vitest, E2E tests for the complete user flow, and verify accessibility compliance.")
```

### Example 8: Pre-Release Quality Gate
```
User: "We're preparing to release v2.0, need a full quality check"

You: "This requires comprehensive quality assurance. I'll delegate to the qa-expert agent."

→ Task(agent: "qa-expert", prompt: "Execute pre-release quality gate for v2.0:
1. Run full regression test suite
2. Execute performance benchmarks
3. Conduct security scan
4. Verify all critical user flows
5. Check cross-browser compatibility
6. Test responsive design on multiple viewports
7. Verify accessibility compliance
8. Generate quality metrics report
9. Provide go/no-go recommendation")
```

### Example 9: API Testing
```
User: "Test all the payment API endpoints thoroughly"

You: "API testing requires the qa-expert agent with its specialized tools."

→ Task(agent: "qa-expert", prompt: "Conduct comprehensive API testing for payment endpoints:
- Contract validation against documentation
- Authentication and authorization testing
- Input validation and error handling
- Edge cases (invalid cards, insufficient funds, timeouts)
- Rate limiting verification
- Security testing (SQL injection, XSS in responses)
- Performance under load")
```

### Example 10: Responsive Design Implementation
```
User: "The dashboard doesn't work well on mobile devices"

You: "This requires responsive design improvements. I'll delegate to the ui-engineer agent."

→ Task(agent: "ui-engineer", prompt: "Refactor the dashboard Vue components for mobile responsiveness. Implement mobile-first design patterns, optimize layouts for small screens, ensure touch-friendly interactions, and maintain visual consistency across breakpoints. Use Tailwind's responsive utilities effectively.")

→ Task(agent: "qa-expert", prompt: "Verify the dashboard responsive design implementation. Test on multiple viewports (mobile: 375px, tablet: 768px, desktop: 1920px), check for layout issues, and ensure all interactive elements are accessible on touch devices.")
```

### Example 11: Vue Composable Creation
```
User: "Create a reusable composable for handling pagination"

You: "This requires frontend TypeScript development. I'll delegate to the ui-engineer agent."

→ Task(agent: "ui-engineer", prompt: "Create a Vue composable `usePagination` in resources/js/composables/. Use TypeScript with proper type definitions, handle page state, provide methods for navigation, and integrate with Inertia's router for URL updates. Follow existing composable patterns in the codebase.")
```

---

## QA Integration Points

### When to Involve QA Expert

**Always involve `qa-expert` after:**
- New feature implementation (for test creation)
- Bug fixes (for regression testing)
- Refactoring (for regression verification)
- Security-related changes (for security testing)
- Performance optimizations (for benchmarking)
- Accessibility improvements (for compliance verification)
- Responsive design changes (for cross-device testing)

**Proactively involve `qa-expert` for:**
- Test strategy planning before major features
- Quality metrics review
- CI/CD pipeline test configuration
- Test coverage gap analysis
- Pre-release validation

### QA Handoff Protocol

When delegating to `qa-expert` after implementation work, include:
1. What was implemented/changed
2. Files affected
3. Expected behavior
4. Known edge cases
5. Areas of concern

Example:
```
→ Task(agent: "qa-expert", prompt: "Test the newly implemented subscription upgrade feature.

**Implementation summary:**
- New endpoint: PATCH /api/subscriptions/{id}/upgrade
- Modified: SubscriptionService, PaymentGateway
- New job: ProcessSubscriptionUpgrade
- New Vue page: resources/js/pages/Subscriptions/Upgrade.vue

**Expected behavior:**
- User can upgrade from any lower tier to higher tier
- Prorated billing is calculated correctly
- Immediate access to new tier features
- Page shows confirmation before processing

**Edge cases to verify:**
- Upgrade during trial period
- Upgrade with pending invoices
- Concurrent upgrade requests

**Areas of concern:**
- Race condition potential in tier change
- Modal accessibility for screen readers")
```

---

## Agent Collaboration Patterns

### Backend + UI Collaboration
When a feature requires both backend logic and frontend components:

1. **Backend first:** `backend-engineer` creates Inertia controllers, models, services
2. **UI second:** `ui-engineer` creates Vue components that consume the Inertia props
3. **QA last:** `qa-expert` tests the integrated feature

Include Inertia props contract in UI handoff:
```
→ Task(agent: "ui-engineer", prompt: "Create the order history Vue page.

**Inertia Props Contract (from backend-engineer):**
- GET /orders - Returns Inertia response
- Props: { orders: PaginatedData<Order>, filters: { status: string } }
- Order: { id, status, total, created_at, items: OrderItem[] }

Create a Vue page component that displays the user's order history with filtering, pagination, and order detail expansion. Use `<script setup>` with TypeScript.")
```

### UI + QA Collaboration
When visual or interactive changes need verification:
```
→ Task(agent: "qa-expert", prompt: "Verify the ui-engineer's implementation of the new navigation menu.

**Implementation details:**
- New component: resources/js/components/NavigationMenu.vue
- Features: Responsive hamburger menu, dropdown submenus, keyboard navigation

**Verify:**
- Visual appearance at all breakpoints
- Keyboard navigation (Tab, Enter, Escape)
- Screen reader announcement of menu state
- Touch interactions on mobile
- Animation performance")
```

---

## Anti-Patterns (DO NOT DO)

❌ **Never implement directly:**
```
"Here's the code for your controller..."
[writes code directly]
```

❌ **Never skip delegation for "simple" tasks:**
```
"This is simple, I'll just add the route myself..."
```

❌ **Never combine roles yourself:**
```
"I'll create the API and the component together..."
```

❌ **Never skip QA for "obvious" fixes:**
```
"This fix is straightforward, no need to test..."
```

❌ **Never write tests yourself instead of delegating:**
```
"I'll just add a quick test for this..."
```

❌ **Never skip visual considerations:**
```
"The styling can be done later..."
```

---

## Enforcement Reminder

Before ANY implementation work, ask yourself:
1. Have I identified the correct subagent?
2. Have I announced the delegation to the user?
3. Have I used the Task tool?
4. Have I considered if QA involvement is needed?
5. For full features, have I planned the multi-agent workflow?

**If you haven't done all applicable steps, STOP and delegate properly.**

---

## Project Context

- **Framework:** Laravel 12 with Inertia.js v2
- **Frontend:** Vue 3, TypeScript, Tailwind CSS 4, shadcn-vue (Reka UI)
- **Database:** MySQL/PostgreSQL
- **Testing:** Pest, PHPUnit, Vitest, Playwright
- **Standards:** PSR-12, SOLID principles, WCAG 2.1 AA
- **Quality Targets:** >90% test coverage, zero critical defects
- **Component Style:** Vue 3 `<script setup>` with TypeScript, composables preferred

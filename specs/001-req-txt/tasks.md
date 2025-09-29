# Tasks: 项目管理平台

**Input**: Design documents from `/specs/001-req-txt/`
**Prerequisites**: plan.md (required), research.md, data-model.md, contracts/

## Execution Flow (main)
```
1. Load plan.md from feature directory
   → If not found: ERROR "No implementation plan found"
   → Extract: tech stack, libraries, structure
2. Load optional design documents:
   → data-model.md: Extract entities → model tasks
   → contracts/: Each file → contract test task
   → research.md: Extract decisions → setup tasks
3. Generate tasks by category:
   → Setup: project init, dependencies, linting
   → Tests: contract tests, integration tests
   → Core: models, services, CLI commands
   → Integration: DB, middleware, logging
   → Polish: unit tests, performance, docs
4. Apply task rules:
   → Different files = mark [P] for parallel
   → Same file = sequential (no [P])
   → Tests before implementation (TDD)
5. Number tasks sequentially (T001, T002...)
6. Generate dependency graph
7. Create parallel execution examples
8. Validate task completeness:
   → All contracts have tests?
   → All entities have models?
   → All endpoints implemented?
9. Return: SUCCESS (tasks ready for execution)
```

## Format: `[ID] [P?] Description`
- **[P]**: Can run in parallel (different files, no dependencies)
- Include exact file paths in descriptions

## Path Conventions
- **Single project**: `src/`, `tests/` at repository root
- **Web app**: `backend/src/`, `frontend/src/`
- **Mobile**: `api/src/`, `ios/src/` or `android/src/`
- Paths shown below assume web app - based on plan.md structure

## Phase 3.1: Setup
- [ ] T001 Create project structure per implementation plan (backend/ and frontend/ directories)
- [ ] T002 Initialize Node.js backend project with Express.js and TypeScript dependencies
- [ ] T003 Initialize React frontend project with TypeScript dependencies
- [ ] T004 [P] Configure ESLint and Prettier for code quality
- [ ] T005 [P] Configure Jest for testing
- [ ] T006 [P] Set up database configuration (SQLite for development, PostgreSQL for production)

## Phase 3.2: Tests First (TDD) ⚠️ MUST COMPLETE BEFORE 3.3
**CRITICAL: These tests MUST be written and MUST FAIL before ANY implementation**

### Contract Tests
- [ ] T007 [P] Contract test GET /api/users in backend/tests/contract/test_users_api.py
- [ ] T008 [P] Contract test GET /api/projects in backend/tests/contract/test_projects_api.py
- [ ] T009 [P] Contract test GET /api/projects/{projectId}/tasks in backend/tests/contract/test_tasks_api.py
- [ ] T010 [P] Contract test GET /api/tasks/{taskId}/comments in backend/tests/contract/test_comments_api.py
- [ ] T011 [P] Contract test GET /api/projects/{projectId}/kanban in backend/tests/contract/test_kanban_api.py

### Integration Tests
- [ ] T012 [P] Integration test user selection flow in backend/tests/integration/test_user_selection.py
- [ ] T013 [P] Integration test project management in backend/tests/integration/test_project_management.py
- [ ] T014 [P] Integration test task movement in backend/tests/integration/test_task_movement.py
- [ ] T015 [P] Integration test comment management in backend/tests/integration/test_comment_management.py
- [ ] T016 [P] Integration test kanban board display in backend/tests/integration/test_kanban_display.py

### Frontend Tests
- [ ] T017 [P] Test user selection UI in frontend/tests/components/test_user_selection.test.tsx
- [ ] T018 [P] Test project list UI in frontend/tests/components/test_project_list.test.tsx
- [ ] T019 [P] Test kanban board UI in frontend/tests/components/test_kanban_board.test.tsx
- [ ] T020 [P] Test task card UI in frontend/tests/components/test_task_card.test.tsx
- [ ] T021 [P] Test comment section UI in frontend/tests/components/test_comment_section.test.tsx

## Phase 3.3: Core Implementation (ONLY after tests are failing)

### Backend Models
- [ ] T022 [P] User model in backend/src/models/user.ts
- [ ] T023 [P] Project model in backend/src/models/project.ts
- [ ] T024 [P] Task model in backend/src/models/task.ts
- [ ] T025 [P] Comment model in backend/src/models/comment.ts
- [ ] T026 [P] KanbanBoard model in backend/src/models/kanbanBoard.ts

### Backend Services
- [ ] T027 [P] UserService CRUD operations in backend/src/services/userService.ts
- [ ] T028 [P] ProjectService CRUD operations in backend/src/services/projectService.ts
- [ ] T029 [P] TaskService CRUD operations in backend/src/services/taskService.ts
- [ ] T030 [P] CommentService CRUD operations in backend/src/services/commentService.ts
- [ ] T031 [P] KanbanService operations in backend/src/services/kanbanService.ts

### Backend API Endpoints
- [ ] T032 GET /api/users endpoint in backend/src/api/users.ts
- [ ] T033 GET /api/projects endpoint in backend/src/api/projects.ts
- [ ] T034 GET /api/projects/{projectId} endpoint in backend/src/api/projects.ts
- [ ] T035 POST /api/projects endpoint in backend/src/api/projects.ts
- [ ] T036 GET /api/projects/{projectId}/tasks endpoint in backend/src/api/tasks.ts
- [ ] T037 POST /api/projects/{projectId}/tasks endpoint in backend/src/api/tasks.ts
- [ ] T038 GET /api/tasks/{taskId} endpoint in backend/src/api/tasks.ts
- [ ] T039 PUT /api/tasks/{taskId} endpoint in backend/src/api/tasks.ts
- [ ] T040 DELETE /api/tasks/{taskId} endpoint in backend/src/api/tasks.ts
- [ ] T041 POST /api/tasks/{taskId}/move endpoint in backend/src/api/tasks.ts
- [ ] T042 GET /api/tasks/{taskId}/comments endpoint in backend/src/api/comments.ts
- [ ] T043 POST /api/tasks/{taskId}/comments endpoint in backend/src/api/comments.ts
- [ ] T044 GET /api/comments/{commentId} endpoint in backend/src/api/comments.ts
- [ ] T045 PUT /api/comments/{commentId} endpoint in backend/src/api/comments.ts
- [ ] T046 DELETE /api/comments/{commentId} endpoint in backend/src/api/comments.ts
- [ ] T047 GET /api/projects/{projectId}/kanban endpoint in backend/src/api/kanban.ts

### Frontend Components
- [ ] T048 [P] User selection page in frontend/src/components/UserSelection.tsx
- [ ] T049 [P] Project list page in frontend/src/components/ProjectList.tsx
- [ ] T050 [P] Kanban board component in frontend/src/components/KanbanBoard.tsx
- [ ] T051 [P] Task card component in frontend/src/components/TaskCard.tsx
- [ ] T052 [P] Comment section component in frontend/src/components/CommentSection.tsx
- [ ] T053 [P] Task detail modal in frontend/src/components/TaskDetailModal.tsx

## Phase 3.4: Integration
- [ ] T054 Connect models to database (SQLite/PostgreSQL)
- [ ] T055 Implement authentication middleware (session-based)
- [ ] T056 Add request/response logging
- [ ] T057 Implement drag and drop functionality for task movement
- [ ] T058 Add real-time updates for task changes
- [ ] T059 Implement data validation and error handling

## Phase 3.5: Polish
- [ ] T060 [P] Unit tests for validation logic in backend/tests/unit/test_validation.py
- [ ] T061 [P] Unit tests for service layer in backend/tests/unit/test_services.py
- [ ] T062 Performance tests (<200ms response time)
- [ ] T063 [P] Update API documentation in docs/api.md
- [ ] T064 [P] Update user guide in docs/user-guide.md
- [ ] T065 Remove code duplication and optimize
- [ ] T066 Run manual testing based on quickstart.md
- [ ] T067 Add loading states and error messages in UI
- [ ] T068 Implement responsive design for different screen sizes

## Dependencies
- Tests (T007-T021) before implementation (T022-T053)
- Model tasks (T022-T026) block service tasks (T027-T031)
- Service tasks (T027-T031) block API endpoint tasks (T032-T047)
- Backend API endpoints (T032-T047) needed for frontend components (T048-T053)
- Implementation before polish (T060-T068)
- T054 blocks T059

## Parallel Example
```
# Launch T007-T011 together (contract tests):
Task: "Contract test GET /api/users in backend/tests/contract/test_users_api.py"
Task: "Contract test GET /api/projects in backend/tests/contract/test_projects_api.py"
Task: "Contract test GET /api/projects/{projectId}/tasks in backend/tests/contract/test_tasks_api.py"
Task: "Contract test GET /api/tasks/{taskId}/comments in backend/tests/contract/test_comments_api.py"
Task: "Contract test GET /api/projects/{projectId}/kanban in backend/tests/contract/test_kanban_api.py"

# Launch T022-T026 together (models):
Task: "User model in backend/src/models/user.ts"
Task: "Project model in backend/src/models/project.ts"
Task: "Task model in backend/src/models/task.ts"
Task: "Comment model in backend/src/models/comment.ts"
Task: "KanbanBoard model in backend/src/models/kanbanBoard.ts"
```

## Notes
- [P] tasks = different files, no dependencies
- Verify tests fail before implementing
- Commit after each task
- Avoid: vague tasks, same file conflicts

## Task Generation Rules
*Applied during main() execution*

1. **From Contracts**:
   - Each contract file → contract test task [P]
   - Each endpoint → implementation task

2. **From Data Model**:
   - Each entity → model creation task [P]
   - Relationships → service layer tasks

3. **From User Stories**:
   - Each story → integration test [P]
   - Quickstart scenarios → validation tasks

4. **Ordering**:
   - Setup → Tests → Models → Services → Endpoints → Components → Polish
   - Dependencies block parallel execution

## Validation Checklist
*GATE: Checked by main() before returning*

- [x] All contracts have corresponding tests
- [x] All entities have model tasks
- [x] All tests come before implementation
- [x] Parallel tasks truly independent
- [x] Each task specifies exact file path
- [x] No task modifies same file as another [P] task
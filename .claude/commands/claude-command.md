---
description: Create a new Claude Code slash command that strictly conforms to the spec
allowed-tools: Write, Read, Glob
model: sonnet
argument-hint: <command-name> [description]
---

# Create Claude Code Slash Command

Create a new slash command in `.claude/commands/` that strictly follows the Claude Code slash command specification.

## Slash Command Specification Reference

**IMPORTANT**: All commands created by this tool MUST conform to the following specification:

### Core Syntax
- Commands use pattern `/<command-name> [arguments]`
- Command names derive from markdown filename (without `.md` extension)
- Store in `.claude/commands/` for project commands or `~/.claude/commands/` for personal commands

### Frontmatter (YAML)
Commands support optional YAML frontmatter with these fields:

| Field | Purpose | Required |
|-------|---------|----------|
| `description` | Brief explanation of command; uses first prompt line if omitted | Recommended |
| `allowed-tools` | Specifies which tools the command can use; inherits from conversation if omitted | Optional |
| `argument-hint` | Describes expected arguments (shown during auto-completion) | Optional |
| `model` | Designates specific model (sonnet, opus, haiku); inherits from conversation if omitted | Optional |
| `disable-model-invocation` | Set to `true` to prevent SlashCommand tool from invoking this command | Optional |

### Argument Handling
- `$ARGUMENTS` - captures all arguments as a single string
- `$1`, `$2`, etc. - access individual positional parameters (like shell scripts)
- Use positional parameters when you need to access arguments individually or provide defaults

### Advanced Features
- **Bash execution**: Prefix with exclamation mark to execute bash before command runs (e.g., exclamation-date +%Y-%m-%d surrounded by backticks)
  - MUST include Bash tool in `allowed-tools` with specific command like `Bash(date:*)`
- **File references**: Use `@filename` to include file contents
- **Namespacing**: Organize in subdirectories (appears in description, not command name)

### Tool Specification Format
When specifying tools in `allowed-tools`:
- Basic tools: `Write, Read, Glob, Edit, WebFetch, etc.`
- Bash with specific commands: `Bash(date:*), Bash(mkdir:*), Bash(git:*)`
- Use wildcards for command families: `Bash(git:*)` allows all git commands

## Command Creation Process

### Step 1: Get Command Details

If arguments were provided:
- Command name: `$1`
- Description: `$2` (or remaining arguments as `$ARGUMENTS`)

If no arguments, ask the user:
1. **Command name** (will become `/command-name`): What should the command be called?
2. **Brief description** (one sentence): What does this command do?
3. **Which tools** will the command need? (Write, Read, Bash, WebFetch, etc.)
4. **Will it use bash execution?** If yes, which specific bash commands?
5. **Does it take arguments?** If yes, what kind (single string or multiple positional)?
6. **Which model** should it use? (sonnet/opus/haiku, or inherit from conversation)

### Step 2: Validate Command Name

Check if `.claude/commands/$1.md` already exists:
- If exists, ask user if they want to overwrite or create a new name
- Command names should be lowercase, use hyphens for spaces
- Examples: `review-pr`, `deploy-staging`, `garden-diary`

### Step 3: Build Frontmatter

Create YAML frontmatter based on user responses:

```yaml
---
description: [One sentence description]
allowed-tools: [Comma-separated list of tools]
model: [sonnet|opus|haiku] (optional)
argument-hint: [Description of expected arguments] (if command takes arguments)
---
```

**Examples of proper frontmatter**:

Simple command with basic tools:
```yaml
---
description: Review the current pull request and suggest improvements
allowed-tools: Read, Bash(gh:*)
model: sonnet
---
```

Command with bash execution:
```yaml
---
description: Create a new diary entry with auto-fetched weather
allowed-tools: Write, Read, Bash(date:*), Bash(mkdir:*), WebFetch
model: sonnet
---
```

Command with arguments:
```yaml
---
description: Deploy the application to a specified environment
allowed-tools: Bash(git:*), Bash(npm:*), Read
argument-hint: <environment> (staging|production)
model: sonnet
---
```

### Step 4: Build Command Content

After frontmatter, write clear instructions for Claude to follow:

**Structure**:
1. **Title**: `# [Command Purpose]`
2. **Overview**: Brief description of what command will do
3. **Step-by-step instructions**: Number each step clearly
4. **Use bash execution syntax**: When needed, show exclamation-mark prefix with the command in backticks
5. **Reference files**: Use `@filename` syntax when referring to specific files
6. **Show example output format**: If creating files, show markdown template

**Best Practices**:
- Be specific and prescriptive (tell Claude exactly what to do)
- Include error handling (what if file doesn't exist, etc.)
- Show expected output formats with markdown templates
- Use clear section headers with `##`
- Reference argument variables: "Use `$1` as the environment name"

### Step 5: Write Command File

Write the complete command to `.claude/commands/$1.md`:

```markdown
---
description: [description]
allowed-tools: [tools]
[other frontmatter fields as needed]
---

# [Command Title]

[Clear description of what this command does]

## Step 1: [First Action]

[Detailed instructions...]

## Step 2: [Next Action]

[More instructions...]

[Continue with all steps...]
```

### Step 6: Validate & Confirm

After writing the command:
1. Read back the created file to verify it's well-formed
2. Check that:
   - Frontmatter is valid YAML (proper `---` delimiters)
   - All required tools are listed in `allowed-tools`
   - Bash commands have proper tool specs like `Bash(date:*)`
   - Description is concise and clear
   - Instructions are step-by-step and specific
3. Confirm to user: "Created `/command-name` command at `.claude/commands/command-name.md`"
4. Suggest: "Try it with `/command-name [arguments]`"

## Examples of Well-Formed Commands

### Example 1: Simple Command (No Arguments, No Bash)

**File**: `.claude/commands/summarize-changes.md`

Shows frontmatter with:
- description: "Summarize all uncommitted changes in the repository"
- allowed-tools: Bash(git:*), Read
- model: sonnet

Content includes steps to:
1. Get git status using bash execution
2. Get git diff using bash execution
3. Analyze changes and provide summary with:
   - List of modified files
   - Brief summary of what changed
   - Overall theme
   - Suggested commit message

### Example 2: Command with Arguments

**File**: `.claude/commands/create-test.md`

Shows frontmatter with:
- description: "Create a test file for the specified component"
- allowed-tools: Write, Read, Glob
- model: sonnet
- argument-hint: <component-name>

Content uses $1 variable for component name and includes steps to:
1. Validate component exists using Glob pattern
2. Read component file to understand structure
3. Create test file with .test.tsx extension including:
   - Component imports and testing library
   - Test suite with describe block
   - Tests for main functionality
   - Tests for edge cases

### Example 3: Command with Bash Execution and File References

**File**: `.claude/commands/deploy.md`

Shows frontmatter with:
- description: "Deploy application to specified environment after running tests"
- allowed-tools: Bash(npm:*), Bash(git:*), Read
- model: sonnet
- argument-hint: <environment> (staging|production)

Content uses $1 for environment and includes steps to:
1. Validate environment is "staging" or "production"
2. Check git status using bash execution to ensure clean working directory
3. Run tests using bash execution (npm test)
4. Build using bash execution (npm run build)
5. Deploy based on environment using bash execution:
   - Staging: npm run deploy:staging
   - Production: npm run deploy:production
6. Confirm successful deployment with timestamp

This example demonstrates proper use of bash execution with multiple commands and argument validation.

## Common Mistakes to Avoid

1. **Missing tool specifications**: If using bash, MUST include `Bash(command:*)` in `allowed-tools`
2. **Invalid YAML**: Frontmatter must have proper `---` delimiters on both sides
3. **Vague instructions**: Be specific - tell Claude exactly what to do, don't be general
4. **Missing argument handling**: If command takes arguments, document using `$1`, `$2`, or `$ARGUMENTS`
5. **No error handling**: Always consider what happens if file doesn't exist, argument is wrong, etc.

## Now Create the Command

Using the command name from `$1` (if provided) or by asking the user, create a new slash command following ALL of the above specifications.

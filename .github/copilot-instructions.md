# GitHub MCP Demo Project - AI Agent Instructions

## Project Purpose
This is a **demonstration project** for GitHub MCP (Model Context Protocol) Server integration, NOT a production application. The primary goal is showcasing AI-driven DevOps workflows through a deliberately broken World Clock web app.

## Critical Architecture Understanding

### Demo-Specific Bug Pattern
- **Intentional Bug**: Line 7 in `index.html` has `href="styls.css"` (missing 'e') 
- **Purpose**: Creates visually obvious CSS failure for demonstration
- **Fix**: Change to `href="styles.css"` 
- **Impact**: Without fix, page appears completely unstyled

### Core Components
- `index.html`: Single-page World Clock app (contains demo bug)
- `styles.css`: Modern CSS with CSS Grid layout and CSS custom properties
- `script.js`: ES6 class-based WorldClock with timezone handling via `Intl` API
- `.vscode/mcp.json`: MCP server configuration for GitHub integration

## Development Workflow (Demo-Specific)

### GitHub MCP Workflow Demonstration
When assisting with this project, follow this specific demo sequence:

1. **Issue Detection**: Identify the CSS link typo causing styling failure
2. **GitHub Issue Creation**: Use `mcp_github_issue_write` with labels: `bug`, `critical`, `styling`
3. **Branch Creation**: Create `hotfix/css-stylesheet-typo-#{issue-number}` via `mcp_github_create_branch`
4. **Local Fix**: Correct the typo in `index.html` line 7
5. **Pull Request**: Use `mcp_github_create_pull_request` with auto-linking to issue
6. **Merge & Cleanup**: Complete workflow via MCP tools

### Testing Approach
- **Local Development**: Use Live Server extension for immediate visual feedback
- **Visual Validation**: Compare styled vs unstyled page appearance
- **No Unit Tests**: This is a demo project, visual verification is sufficient

## Code Patterns & Conventions

### JavaScript Architecture
- **Class-based**: Single `WorldClock` class in `script.js`
- **Async/Await**: All time operations use modern async patterns
- **No External APIs**: Uses browser `Intl` API and `Date` objects (CORS-free)
- **Global Exposure**: `window.WorldClock = WorldClock` for potential extension

### CSS Patterns
- **CSS Custom Properties**: All colors/spacing defined in `:root`
- **CSS Grid**: `.additional-info` uses auto-fit grid for responsive 4-panel layout
- **Modern Animations**: `@keyframes` for fadeIn effects, `transform` for hover states
- **Mobile-First**: Responsive breakpoints at 768px and 480px

### HTML Structure
- **Semantic HTML**: Proper `header`, `main`, `footer` structure
- **BEM-like Classes**: `.clock-container`, `.info-card`, `.info-value` pattern
- **Accessibility**: Proper heading hierarchy, meaningful alt text

## Integration Points

### GitHub MCP Server
- **Configuration**: `.vscode/mcp.json` defines GitHub MCP endpoint
- **Required Tools**: Uses `mcp_github_*` functions for all GitHub operations
- **Authentication**: Relies on VS Code's GitHub authentication

### External Dependencies
- **Google Fonts**: Inter font family (only external dependency)
- **No Build Process**: Direct file serving, no bundling required
- **No Package Manager**: Pure HTML/CSS/JS, no npm/node_modules

## Key Demo Talking Points

When explaining this project to others:
- Emphasize the **visual impact** of the CSS bug (styled → unstyled)
- Highlight **MCP automation** replacing manual GitHub operations
- Show **complete workflow** from bug detection to deployment
- Demonstrate **AI-human collaboration** in practical DevOps scenarios

## DO NOT
- Add build tools, package.json, or complex dependencies
- Create actual unit tests (demo focuses on visual verification)
- Remove the intentional bug without going through proper MCP workflow
- Add production-ready features (error handling, accessibility improvements)
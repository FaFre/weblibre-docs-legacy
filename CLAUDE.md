# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Quartz v4** static site generator repository for WebLibre documentation. Quartz transforms Markdown files in the [content](content) directory into a fully-featured static website with features like search, graph visualization, backlinks, and Wikipedia-style popovers.

**Documentation**: https://quartz.jzhao.xyz/

## Common Commands

### Development
```bash
# Build and serve the site locally with hot reload
npm run docs

# Build the site (output to public/)
npx quartz build

# Build with verbose output
npx quartz build --verbose

# Build and serve with watch mode
npx quartz build --serve

# Build from a different content directory
npx quartz build -d <directory>
```

### Testing & Quality
```bash
# Run tests
npm test

# Type check without emitting files
npm run check

# Format code
npm run format

# Profile build performance
npm run profile
```

### CLI Commands
The main CLI is at [quartz/bootstrap-cli.mjs](quartz/bootstrap-cli.mjs) and provides these commands:
- `npx quartz create` - Initialize new Quartz project
- `npx quartz update` - Get latest Quartz updates
- `npx quartz restore` - Restore content from cache
- `npx quartz sync` - Sync to/from GitHub
- `npx quartz build` - Build static site

## Architecture

### Build Pipeline (3-Phase Process)

The build system follows a **transformer → filter → emitter** pipeline defined in [quartz/build.ts](quartz/build.ts):

1. **Parse** ([quartz/processors/parse.ts](quartz/processors/parse.ts))
   - Reads Markdown files from content directory
   - Creates unified processors for MD→MD AST and MD AST→HTML AST transformations
   - Uses worker pool for parallel processing
   - Transformers run their `markdownPlugins` and `htmlPlugins` hooks

2. **Filter** ([quartz/processors/filter.ts](quartz/processors/filter.ts))
   - Filters content using `shouldPublish()` method from filter plugins
   - Removes drafts, unpublished content, etc.

3. **Emit** ([quartz/processors/emit.ts](quartz/processors/emit.ts))
   - Generates final HTML pages and static resources
   - Each emitter can implement `emit()` for full builds or `partialEmit()` for incremental rebuilds
   - Runs emitters in parallel

### Plugin System

All functionality is plugin-based. Plugins are defined in [quartz/plugins/](quartz/plugins/) and configured in [quartz.config.ts](quartz.config.ts).

**Three plugin types** ([quartz/plugins/types.ts](quartz/plugins/types.ts)):

- **Transformers** ([quartz/plugins/transformers/](quartz/plugins/transformers/))
  - Transform Markdown/HTML during parsing
  - Can add `markdownPlugins` (remark plugins) and `htmlPlugins` (rehype plugins)
  - Examples: FrontMatter, SyntaxHighlighting, ObsidianFlavoredMarkdown, TableOfContents

- **Filters** ([quartz/plugins/filters/](quartz/plugins/filters/))
  - Determine which content should be published
  - Implement `shouldPublish(ctx, content)` method
  - Example: RemoveDrafts

- **Emitters** ([quartz/plugins/emitters/](quartz/plugins/emitters/))
  - Generate output files (HTML pages, JSON indexes, sitemaps, etc.)
  - Implement `emit()` and optionally `partialEmit()` for incremental builds
  - Examples: ContentPage, FolderPage, TagPage, ContentIndex, Assets

### Component System

UI components are Preact components in [quartz/components/](quartz/components/). Each component:
- Receives `QuartzComponentProps` (defined in [quartz/components/types.ts](quartz/components/types.ts))
- Can export static `css`, `beforeDOMLoaded`, and `afterDOMLoaded` resources
- Is positioned via layout configuration in [quartz.layout.ts](quartz.layout.ts)

**Page components** ([quartz/components/pages/](quartz/components/pages/)):
- [Content.tsx](quartz/components/pages/Content.tsx) - Single content page
- [FolderContent.tsx](quartz/components/pages/FolderContent.tsx) - Folder listing
- [TagContent.tsx](quartz/components/pages/TagContent.tsx) - Tag listing
- [404.tsx](quartz/components/pages/404.tsx) - Not found page

**Layout system** ([quartz.layout.ts](quartz.layout.ts)):
Defines component placement in seven regions:
- `head` - HTML head elements
- `header` - Top of page
- `beforeBody` - Before main content
- `pageBody` - Main content area
- `afterBody` - After main content
- `left` - Left sidebar
- `right` - Right sidebar
- `footer` - Bottom of page

Components are assembled into full pages by [quartz/components/renderPage.tsx](quartz/components/renderPage.tsx).

### Configuration

**[quartz.config.ts](quartz.config.ts)**: Main configuration
- `configuration` - Global settings (pageTitle, theme, analytics, locale, etc.)
- `plugins` - Plugin instances for transformers, filters, and emitters

**[quartz.layout.ts](quartz.layout.ts)**: Layout configuration
- `sharedPageComponents` - Components shared across all pages
- `defaultContentPageLayout` - Layout for single content pages
- `defaultListPageLayout` - Layout for list pages (tags, folders)

**[quartz/cfg.ts](quartz/cfg.ts)**: Type definitions for configuration

### Key Utilities

- [quartz/util/path.ts](quartz/util/path.ts) - Path handling, slugification
- [quartz/util/resources.tsx](quartz/util/resources.tsx) - Static resource management (CSS/JS)
- [quartz/util/theme.ts](quartz/util/theme.ts) - Theme configuration
- [quartz/util/perf.ts](quartz/util/perf.ts) - Performance timing
- [quartz/util/ctx.ts](quartz/util/ctx.ts) - Build context types

### Content Processing

**Markdown Processing**:
- Uses [unified](https://unifiedjs.com/) ecosystem (remark + rehype)
- Markdown → MD AST (remark-parse)
- MD AST transformations via transformer plugins (remark plugins)
- MD AST → HTML AST (remark-rehype)
- HTML AST transformations via transformer plugins (rehype plugins)
- HTML AST → HTML string (hast-util-to-html)

**Supported Features**:
- Obsidian-flavored Markdown (wikilinks, callouts, etc.)
- GitHub-flavored Markdown
- LaTeX math (KaTeX or MathJax)
- Syntax highlighting (Shiki)
- Citations (rehype-citation)
- Table of contents auto-generation

### Incremental Builds

Watch mode ([quartz/build.ts](quartz/build.ts)):
- Uses `chokidar` to watch content directory
- Maintains `ContentMap` of all files and their parsed state
- Tracks changes since last build
- Calls `partialEmit()` on emitters that support incremental rebuilds
- WebSocket connection for browser hot reload

### TypeScript Configuration

- JSX uses Preact (`"jsxImportSource": "preact"`)
- Strict mode enabled
- ES modules (`"module": "esnext"`)
- Node module resolution
- Tests use `tsx --test`

## Development Notes

### Adding a New Plugin

1. Create plugin file in appropriate [quartz/plugins/](quartz/plugins/) subdirectory
2. Implement plugin interface from [quartz/plugins/types.ts](quartz/plugins/types.ts)
3. Export plugin from [quartz/plugins/index.ts](quartz/plugins/index.ts)
4. Add to plugin array in [quartz.config.ts](quartz.config.ts)

### Adding a New Component

1. Create component file in [quartz/components/](quartz/components/)
2. Implement `QuartzComponent` type from [quartz/components/types.ts](quartz/components/types.ts)
3. Export from [quartz/components/index.ts](quartz/components/index.ts)
4. Add to layout in [quartz.layout.ts](quartz.layout.ts)

### Modifying Build Process

Build logic is in [quartz/build.ts](quartz/build.ts). The three processors are:
- [quartz/processors/parse.ts](quartz/processors/parse.ts) - Parsing and transformation
- [quartz/processors/filter.ts](quartz/processors/filter.ts) - Content filtering
- [quartz/processors/emit.ts](quartz/processors/emit.ts) - File emission

### Content Location

All content Markdown files should be in the [content](content) directory (or specified with `-d` flag). The [docs](docs) directory is for Quartz's own documentation.
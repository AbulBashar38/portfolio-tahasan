# AI Coding Assistant Instructions for React Portfolio Template

## Project Overview

This is a customizable React portfolio template built with Vite, featuring a data-driven architecture where content is managed through JSON files in `public/data/`. The app supports multiple languages, themes, and responsive design with Bootstrap 5.

## Architecture

- **Framework**: React 18 with Vite for build tooling
- **Data Layer**: JSON-based configuration in `public/data/` (settings, profile, sections, strings)
- **Component Structure**: Modular components in `src/components/` organized by type (articles, sections, providers)
- **State Management**: Multiple React Context providers (DataProvider, LanguageProvider, ThemeProvider, etc.)
- **Styling**: SCSS with Bootstrap 5, custom styles in `src/styles/`
- **Internationalization**: Built-in multi-language support via locale objects in JSON data

## Key Directories & Files

- `public/data/settings.json` - Core app configuration (themes, languages, debug settings)
- `public/data/sections/` - Content data for portfolio sections (skills, experience, portfolio, etc.)
- `src/components/articles/` - Reusable article components (ArticleSkills, ArticleTimeline, etc.)
- `src/providers/` - React Context providers for global state
- `src/hooks/` - Custom hooks for utilities and API interactions
- `npm/` - Custom Node.js scripts for content management

## Development Workflows

- **Local Development**: `npm run dev` (Vite dev server)
- **Build**: `npm run build` (produces `dist/` for deployment)
- **Linting**: `npm run lint` (ESLint with React rules)
- **Create Article Component**: `npm run resume:make:article ArticleName` (generates JSX/SCSS files)
- **Clear Resume Data**: `npm run resume:clear` (resets portfolio content)
- **Deployment**: GitHub Actions workflow deploys to GitHub Pages on push to main branch

## Coding Patterns & Conventions

### Article Components

- **Naming**: Always start with "Article" (e.g., `ArticleSkills.jsx`)
- **Structure**: Each article has matching `.jsx` and `.scss` files
- **Data Binding**: Components receive `article` prop with JSON data from sections
- **Styling**: Import base styles with `@import "/src/styles/extend.scss";`
- **Example**:
  ```jsx
  const ArticleSkills = ({ article }) => {
    return (
      <div className="article-skills">
        {article.items.map((item) => (
          <div key={item.id}>{item.locales.en.title}</div>
        ))}
      </div>
    );
  };
  ```

### Data Structure

- **Locales**: All user-facing text uses locale objects: `{"en": {"title": "Skills"}, "es": {"title": "Habilidades"}}`
- **Article Schema**: Sections contain `articles` array with `component`, `settings`, and `items`
- **Settings**: Control sorting, display options via `settings` object in articles
- **Items**: Content arrays with `id`, `locales`, and component-specific fields

### Provider Pattern

- **Usage**: Wrap components with providers from `src/providers/`
- **Data Access**: Use `useData()` for content, `useLanguage()` for i18n
- **Example**:

  ```jsx
  import { useData } from "/src/providers/DataProvider.jsx";

  const MyComponent = () => {
    const { getSection } = useData();
    const skillsSection = getSection("skills");
    // ...
  };
  ```

### Email Integration

- **Service**: EmailJS for contact form (`@emailjs/browser`)
- **Configuration**: Set service ID, template ID, public key in settings
- **Validation**: Use `useApi().validators.validateEmailRequest()` for form validation

## Common Tasks

- **Add New Section**: Create JSON file in `public/data/sections/`, add to categories in `categories.json`
- **Customize Styling**: Modify SCSS variables in `src/styles/`, use Bootstrap classes
- **Add Language**: Add locale objects to all JSON files, update `supportedLanguages` in settings
- **Create Article Type**: Use `npm run resume:make:article`, implement rendering logic for JSON data
- **Theme Customization**: Modify CSS custom properties in theme files

## Integration Points

- **EmailJS**: Contact form sending (configure in settings)
- **Font Awesome**: Icons via `faIcon` fields in data
- **Swiper**: Sliders/carousels in portfolio sections
- **Smooth Scrollbar**: Custom scrollbar behavior

## Deployment

- **Platform**: GitHub Pages
- **Trigger**: Push to `main` branch or manual workflow dispatch
- **Build Output**: `dist/` directory
- **Base Path**: Configure in `vite.config.js` if deploying to subdirectory

## Debugging

- Enable `debugMode` in `settings.json` to skip animations during development
- Use `fakeEmailRequests` to simulate contact form without sending real emails
- Check browser console for data loading errors from `public/data/`</content>
  <parameter name="filePath">/Users/abulbasar/Desktop/portfolio-tahasan/.github/copilot-instructions.md

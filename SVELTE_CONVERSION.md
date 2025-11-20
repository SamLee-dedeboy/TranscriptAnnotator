# Transcript Annotator - Svelte 5 Conversion

This project has been converted from pure HTML/JavaScript to Svelte 5 using runes for modern reactive programming.

## Project Structure

The application is now split into modular Svelte components:

- **`src/App.svelte`** - Main application component that manages global state and coordinates between components
- **`src/lib/LeftSidebar.svelte`** - Transcript list and speaker filter controls
- **`src/lib/MainContent.svelte`** - Main transcript display with message selection and annotation form
- **`src/lib/RightSidebar.svelte`** - Saved annotations display
- **`src/constants.ts`** - TypeScript type definitions and constants

## Key Features Converted

### State Management (Svelte 5 Runes)
- `$state()` - For reactive local state
- `$derived()` - For computed values
- `$props()` - For component properties
- `$bindable()` - For two-way data binding

### Functionality
- ✅ Transcript loading from server
- ✅ Speaker filtering and color customization
- ✅ Text selection for annotations
- ✅ Annotation creation, display, and deletion
- ✅ Responsive layout with three-column design

### Interactive Features
- ✅ Click and drag text selection
- ✅ Real-time annotation form display
- ✅ Speaker visibility toggle
- ✅ Annotation management

## API Integration

The app expects a backend server running on `http://localhost:5000` with the following endpoints:

- `GET /transcripts` - List available transcripts
- `GET /transcripts/{filename}/segmented` - Get segmented transcript content
- `GET /annotations/{filename}` - Get annotations for a transcript
- `POST /annotations/{filename}` - Save new annotation
- `DELETE /annotations/{filename}/{id}` - Delete annotation

## Development

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

## Changes from Original HTML

### Architecture Improvements
- **Component-based**: Split into logical, reusable components
- **TypeScript**: Full type safety with interfaces for data structures
- **Modern Reactive Programming**: Using Svelte 5 runes instead of manual DOM manipulation
- **Better State Management**: Centralized state with proper reactivity

### Code Quality
- **Accessibility**: Improved keyboard navigation and ARIA labels
- **Performance**: Reactive updates instead of full DOM re-renders
- **Maintainability**: Cleaner separation of concerns
- **Type Safety**: Full TypeScript integration

### Features Enhanced
- **Real-time UI Updates**: Reactive state automatically updates UI
- **Better Error Handling**: Graceful fallbacks for missing data
- **Improved UX**: Smoother interactions and visual feedback
- **Mobile Friendly**: Better responsive design foundation

## Migration Notes

The original `pure_html/index.html` contained ~1800 lines of HTML, CSS, and JavaScript. This has been converted to:
- 4 focused Svelte components (~150-200 lines each)
- Shared TypeScript interfaces
- Modern CSS with component-scoped styles
- Reactive state management

All original functionality has been preserved while improving maintainability and adding type safety.
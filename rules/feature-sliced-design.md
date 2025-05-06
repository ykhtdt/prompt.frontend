Feature-Sliced Design (FSD) Architectural Methodology v2.1

## 1. Layer Structure
  * Layers are the first level of organisational hierarchy in Feature-Sliced Design
  * Their purpose is to separate code based on how much responsibility it needs and how many other modules in the app it depends on.
  * There are 6 layers in total, arranged from most responsibility and dependency to least:

### 1-1. App Layer
  * Role
    - The App Layer is the highest level of the Feature-Sliced Design architecture.
    - It handles application initialization, bootstrapping, and global configuration.
    - Contains everything required to run the application.
  * Characteristics
    - Does not contain slices (unlike other layers)
    - Directly composed of segments
    - Has the highest level of responsibility and dependency
    - Can import from all other layers
    - Other layers cannot import from the App layer
  * Main Segments
    - providers: Global providers and context setup
    - styles: Global styling and theme configuration
    - routes: Application routing configuration
    - entry: Main entry points and initialization code
    - fonts: Global font loading and setup for consistent typography

### 1-2. Pages Layer
  * Role
    - Represents the top-level page views of the application that users directly interact with
  * Characteristics
    - Each page is its own slice (e.g., home, profile, article-read, settings)
    - Cannot reference other pages (cannot import code from other pages)
    - Can only import from layers below (widgets, features, entities, shared)
    - Combines widgets, features and other components to create complete pages
    - Typically contains routing configuration specific to that page
    - May include page-specific layouts, state management, and API interactions
  * Main Segments
    - ui: Page-specific components and layouts
    - api: Page-specific API requests
    - model: Page-specific state and business logic
    - lib: Helper functions and utilities specific to the page
    - config: configuration files and feature flags.

### 1-3. Widgets Layer
  * Role
    - Represents large, self-sufficient blocks of UI that can be reused across multiple pages
    - Provides complex composite components that deliver complete user interface functionality
    - Serves as containers for features and entities to create meaningful UI blocks
  * Characteristics
    - Each widget is its own slice (e.g., header, sidebar, product-card, user-profile)
    - Cannot reference other widgets (cannot import code from other widgets)
    - Can only import from layers below (features, entities, shared)
    - May act as layout containers or complex UI components with their own state
    - Should be extracted when UI blocks are reused across multiple pages or when pages have multiple large independent blocks
    - Can serve as router blocks in nested routing systems, similar to how Pages layer functions in flat routing
  * Main Segments
    - ui: Widget-specific components and layouts
    - api: Widget-specific API requests
    - model: Widget-specific state and business logic
    - lib: Helper functions and utilities specific to the widget
    - config: Configuration files and feature flags

### 1-4. Features Layer
  * Role
    - Represents the main user interactions and business processes in the application
    - Implements reusable functionality that users care about
    - Encapsulates business logic that often involves business entities
  * Characteristics
    - Each feature is its own slice (e.g., auth, comments, notifications, search)
    - Cannot reference other features (cannot import code from other features)
    - Can only import from layers below (entities, shared)
    - Should be extracted when functionality is reused across multiple pages
    - Should be carefully selected to not overwhelm newcomers (not everything needs to be a feature)
    - Helps newcomers quickly discover important areas of functionality
  * Main Segments
    - ui: Feature-specific UI components like forms and interactive elements
    - api: Feature-specific API calls and data handling
    - model: Feature-specific state, validation, and business logic
    - lib: Helper functions and utilities specific to the feature
    - config: Feature flags and configuration settings

### 1-5. Entities Layer
  * Role
    - Represents business entities and domain concepts from the real world
    - Contains the core business models that the application works with
    - Provides data structures and basic visualizations of business objects
  * Characteristics
    - Each entity is its own slice (e.g., user, product, post, comment)
    - Typically represents terms used by the business to describe the product
    - Contains data models, validation schemas, and basic UI representations
    - Can only import from the shared layer
    - May use @x notation for cross-entity relationships while maintaining slice isolation
    - UI components are primarily for consistent representation across the application
  * Main Segments
    - ui: Entity-specific UI components for consistent visual representation
    - api: Entity-specific API requests and data manipulation
    - model: Entity data structures, validation schemas, and business logic
    - lib: Helper functions and utilities specific to the entity
    - @x: Cross-entity imports for managing entity relationships

### 1-6. Shared Layer
  * Role
    - Forms the foundation for the rest of the application
    - Creates connections with the external world (backends, libraries, environment)
    - Provides reusable utilities and core functionality
    - Defines highly contained, focused internal libraries
  * Characteristics
    - Does not contain slices (unlike other middle layers)
    - Directly composed of segments like the App layer
    - Has the lowest level of responsibility and dependency
    - All files can reference and import from each other within the layer
    - Can be imported by all other layers
    - Doesn't depend on business domains or application specifics
  * Main Segments
    - api: API clients and request functions for backend endpoints
    - ui: Application's UI kit and basic components without business logic
    - lib: Focused internal libraries (e.g., for dates, colors, text manipulation)
    - config: Environment variables, global feature flags, and configuration
    - routes: Route constants and patterns for matching routes

## 2. Import rule on layers

### Simple Summary: Code Import Rules

The core rules for importing code in FSD are:

1. **Downward Imports Only**: Always import code only from layers below your current layer.
2. **No Horizontal Imports**: Cannot import code from other slices within the same layer.
3. **Free Internal References**: Freely import code from within your own slice.
4. **App and Shared Exceptions**: These two layers don't have slices, and their segments can freely import from each other.

### Detailed Explanation

#### Layer Import Rules

Layers consist of slices - highly cohesive groups of modules. Dependencies between slices are regulated by the layer import rule:

* A module (file) in a slice can only import from slices located in layers strictly below it.
* For example, a file inside 📁 ~/features/aaa (~/features/aaa/api/request.ts) cannot import code from any file in 📁 ~/features/bbb, but can import from 📁 ~/entities and 📁 ~/shared. It can also import from other files within its own slice 📁 ~/features/aaa (e.g., ~/features/aaa/lib/cache.ts).

#### Special Exceptions: App and Shared Layers

App and Shared layers are exceptions to this rule:
* They function both as layers and as slices simultaneously.
* While slices typically partition code by business domain, Shared has no business domains, and App combines all business domains.
* In practice, this means that App and Shared layers are composed of segments, and these segments can import from each other freely.

#### Import Path Conventions

* **Within the same slice**: Relative paths are preferred to maintain the cohesion and portability of the slice. Example: within the features/auth slice, use `import { validatePassword } from '../lib/validators'` rather than absolute paths.
* **From other layers**: Absolute paths are recommended when importing from other layers to make dependencies clear and explicit. Example: `import { User } from 'entities/user'`
* **From segments in App and Shared layers**: Either relative or absolute paths can be used based on team preference, but consistency should be maintained throughout the project.

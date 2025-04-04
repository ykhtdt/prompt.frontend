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
  * Role: 

### 1-3. Widgets Layer
  * Role:

### 1-4. Features Layer
  * Role:  

### 1-5. Entities Layer
  * Role:  

### 1-6. Shared Layer
  * Role:  
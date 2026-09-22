# Architecture & Technical Overview

This document provides a high-level architectural overview of **ALMADDAH Optics**, detailing the system structure, data flow, and key design decisions.

---

## High-Level System Architecture

The application follows a decoupled client-server pattern. The client interacts with the backend strictly through HTTP requests returning structured JSON payloads.

```mermaid
flowchart TD
    subgraph Client["Client Tier"]
        Browser["Web Browser"]
        StorefrontUI["Storefront UI<br/>(Catalog, Detail, Cart, Checkout)"]
        AdminUI["Admin Panel<br/>(Inventory, Lenses, Orders, Promos)"]
        LocalStorage["Browser Storage<br/>(Cart State & User Session)"]
    end

    subgraph Server["Server Tier (Apache / LiteSpeed)"]
        PublicAPI["Storefront API<br/>(backend/api.php)"]
        AdminAPI["Admin API<br/>(backend/admin_api.php)"]
        Config["Configuration & Schema Verifier<br/>(backend/config.php)"]
    end

    subgraph Persistence["Persistence Tier"]
        MySQL[("MySQL / MariaDB<br/>(InnoDB, utf8mb4)")]
    end

    Browser --> StorefrontUI
    Browser --> AdminUI
    StorefrontUI <--> LocalStorage
    StorefrontUI -->|HTTP GET / POST (JSON)| PublicAPI
    AdminUI -->|HTTP GET / POST (JSON)| AdminAPI
    PublicAPI --> Config
    AdminAPI --> Config
    Config -->|PDO with Prepared Statements| MySQL
```

---

## Application Layers

### 1. Frontend Tier
- **Structure & Markup**: Semantic HTML5 templates organized by user role (`index.html` and `Html/` for the public storefront; `admin/` for the management console).
- **Styling**: Native CSS3 using CSS variables for design tokens (color palettes, typography scales, elevation shadows, and responsive layout breakpoints). No external CSS utility frameworks are used, reducing asset payloads.
- **Client Logic**: Modular ES6+ JavaScript modules handle:
  - Catalog filtering across audience categories (Men, Women, Kids) and frame types (Sunglasses, Optical, Clip-On).
  - Dynamic image galleries synchronized with selected frame color swatches.
  - The prescription lens configuration state engine.
  - Cart persistence via `localStorage` to preserve items across page transitions.

### 2. Application & API Tier
- **Storefront API (`backend/api.php`)**:
  - Handles public read operations: catalog retrieval, product details, active category placements, promo code validation, customer reviews, and site announcement text.
  - Handles order intake: parses incoming order objects (customer contacts, delivery address, ordered items with serialized optical lens data) and persists records transactionally.
- **Admin API (`backend/admin_api.php`)**:
  - Provides administrative endpoints for inventory CRUD operations, image file uploads, lens catalog management (brands, types, coatings), promo code administration, and order fulfillment status updates.
- **Database Connection & Initialization (`backend/config.php`)**:
  - Centralizes the PDO connection using environment variables (`DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, `DB_PASSWORD`).
  - The application checks required database tables and columns during initialization and applies the necessary schema updates.

### 3. Persistence Tier
- **MySQL / MariaDB**:
  - Configured with `InnoDB` storage engine for ACID transaction support and foreign key constraints (e.g., cascading deletes on order items).
  - Uses `utf8mb4_unicode_ci` character encoding to support multilingual product descriptions and customer details.

---

## Key Architectural Decisions

### Native Frontend vs. Single-Page Application (SPA) Frameworks
- **Decision**: Implemented using modular vanilla JavaScript without React, Vue, or Angular.
- **Rationale**: For an e-commerce catalog with targeted interactive components (lens configurator, cart drawer, gallery), native JavaScript minimizes initial JavaScript parsing time, eliminates build-step compilation overhead, and performs reliably on lower-powered mobile devices over cellular networks.

### Unified Cart & Order Payload
- **Decision**: Prescription lens specifications are encapsulated directly inside each order item payload rather than treated as disconnected products.
- **Rationale**: Eyewear frames and their prescription lenses are physically coupled. When an order item is created, it stores the base frame price, lens brand name, lens type name, selected coating list, and additional lens fee as a single item entry. This prevents orphaned lens configurations and simplifies admin order review.

### Database Parameterization & Security
- **Decision**: All database queries utilize PDO prepared statements with explicit parameter binding.
- **Rationale**: Prevents SQL injection vulnerabilities across all user-supplied input fields (checkout inputs, search terms, and admin forms). Input sanitization routines escape output rendered into the DOM to guard against cross-site scripting (XSS).

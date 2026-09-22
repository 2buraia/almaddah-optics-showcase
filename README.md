# ALMADDAH Optics

Luxury Eyewear & Custom Lens E-Commerce Platform

A bespoke web platform and administrative control center designed for optical retailers, enabling customers to order designer frames, configure certified prescription lenses, and select clip-on attachments with real-time pricing and delivery tracking.

## Project Overview

| | |
|---|---|
| **Status** | Production |
| **Platform** | Responsive Web Application |
| **Architecture** | REST API · Modular Frontend |
| **Source Code** | Private Repository |
| **Deployment** | Hostinger |

## About the Project

ALMADDAH Optics is a commercial e-commerce storefront and store administration platform designed specifically for the optical retail market.

Unlike standard retail stores that sell fixed-SKU products, prescription eyewear requires handling multiple dependent variables per purchase: frame selection, medical lens specifications, manufacturer brand tiers, and surface treatments. This application solves that complexity by integrating a step-by-step prescription lens studio into the product purchasing flow, automatically calculating combined pricing and passing structured optical details through to order fulfillment.

The platform serves two primary audiences:
- **Customers**: Browse collections (Men, Women, Kids), filter by frame utility (Sunglasses, Optical, Clip-On), configure prescription lenses with real-time pricing, and place orders via Cash on Delivery.
- **Store Administrators**: Manage product catalogs, maintain lens brand pricing matrices, organize category placements, track incoming orders with full prescription specifications, and manage promotions.

## Key Features

- **Prescription Lens Configuration**: Interactive studio supporting certified lens brands (Essilor, ZEISS, Crizal, HOYA), lens types (Single Vision, Bifocal, Progressive), and optical coatings (Anti-Reflective, Blue Cut, Hydrophobic, Hard Coat, UV400).
- **Intelligent Category Filtering**: Category browser across Men, Women, and Kids collections with instant subcategory filtering for Sunglasses, Optical & Eyeglasses, and Clip-On frames.
- **Dynamic Product Gallery**: High-resolution image viewer with interactive thumbnail switching and color-variant synchronization.
- **Transparent Cart & Checkout**: Persistent cart management displaying itemized breakdowns of frame and lens additions, paired with a one-page Cash on Delivery checkout and promo code validation.
- **Administrative Control Panel**: Secure management interface for catalog inventory, lens pricing rules, category routing, customer review curation, and order inspection.
- **Announcement Marquee**: Dynamic top-bar ticker for store notifications and seasonal messaging, editable through the administration portal.

## Screenshots

### Storefront Homepage
![Storefront Homepage](screenshots/home.png)

### Eyewear Collection Browser
![Eyewear Collection Browser](screenshots/catalog.png)

### Prescription Lens Studio
![Prescription Lens Studio](screenshots/product_lenses.png)

### Shopping Bag
![Shopping Bag](screenshots/cart.png)

### Mobile Experience
<p align="center">
  <img src="screenshots/mobile.png" alt="Mobile Experience" width="360" />
</p>

## Technology

| Layer | Technology |
|---|---|
| **Frontend** | Vanilla JavaScript (ES6+), Semantic HTML5, Custom CSS3 Design System |
| **Backend** | PHP 8.x (Stateless REST API) |
| **Database** | MySQL / MariaDB (InnoDB, `utf8mb4_unicode_ci`) |
| **Typography & Icons** | Playfair Display, Inter, Font Awesome 6.5.2 |
| **Web Server** | Apache / LiteSpeed |
| **Hosting** | Hostinger Cloud |

## Architecture

The application follows a decoupled client-server architecture:
- **Stateless RESTful API**: Structured endpoints handle product catalog queries, category metadata, order submission, and administrative operations using JSON payloads and parameterized PDO statements to prevent SQL injection.
- **Modular Client Architecture**: Storefront and admin interfaces are organized into focused JavaScript modules managing DOM updates, shopping cart state persistence via browser storage, and real-time pricing calculations without framework bloat.
- **Automated Schema Provisioning**: A self-healing database initialization layer automatically checks table schemas, applies required column migrations, and verifies default catalog records upon environment initialization.

## Live Project

View the live application: [peru-falcon-934987.hostingersite.com](https://peru-falcon-934987.hostingersite.com)

## Source Code

> The application source code is maintained in a private repository.

## Project Status

Active production deployment. Maintained and monitored for performance, compatibility, and catalog updates.

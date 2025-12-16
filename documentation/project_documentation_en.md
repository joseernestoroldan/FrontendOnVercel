# StoreFrontend Documentation

**A Modern React Application for Product Management**

## Overview

**StoreFrontend** is a sleek and modern web application designed for managing a product inventory. Built with **React** and powered by **Vite**, it offers a fast and responsive user experience. The UI is crafted using **Chakra UI**, providing a consistent and accessible design system with built-in dark mode support.

The application allows users to view a list of products, add new products, update existing ones, and delete them. It interacts with an external Express.js API hosted on Vercel.

## Technology Stack

- **Frontend Framework:** React 18
- **Build Tool:** Vite
- **UI Library:** Chakra UI (v3) with Emotion
- **State Management:** Zustand
- **Routing:** React Router (v7)
- **Icons:** React Icons
- **Animations:** Framer Motion
- **Theme:** Next-themes for Dark/Light mode

## Installation & Setup

Follow these steps to set up the project locally:

1. **Clone the repository:**

   ```bash
   git clone https://github.com/yourusername/StoreFrontend.git
   cd StoreFrontend
   ```

2. **Install dependencies:**

   ```bash
   npm install
   ```

3. **Run the development server:**

   ```bash
   npm run dev
   ```

4. Open `http://localhost:5173` (or the port shown in your terminal) to view the app.

## Project Structure

```tree
src/
├── components/          # Reusable UI components
│   ├── ui/              # Chakra UI specific components (snippets)
│   ├── Modal.jsx        # Product update modal
│   ├── Navbar.jsx       # Top navigation bar
│   └── ProductCard.jsx  # Individual product display card
├── pages/               # Route-level components
│   ├── CreatePage.jsx   # Page for creating new products
│   └── HomePage.jsx     # Main landing page listing products
├── store/               # Global state management
│   └── product.js       # Zustand store for product operations
├── App.jsx              # Main application layout and routes
└── main.jsx             # Entry point wrapping App with providers
```

## Component Breakdown

### Navbar (`src/components/Navbar.jsx`)

The navigation header. It features:

- **Responsive Design:** Adapts to mobile and desktop screens.
- **Theme Toggle:** Switches between Light and Dark mode using `useColorMode`.
- **Creation Link:** Quick access to the "Create Product" page.

### ProductCard (`src/components/ProductCard.jsx`)

Displays individual product information including image, name, and price. It includes action buttons for:

- **Editing:** Opens the `Modal` component.
- **Deleting:** Triggers the `deleteProduct` action from the store.

_Design Note:_ Uses a glassmorphism effect in the UI (`backdropBlur`).

### Modal (`src/components/Modal.jsx`)

A dialog component built with Chakra UI's Dialog primitives. It handles the **Update** functionality. It manages its own local state for the form inputs before syncing with the global store upon submission.

### CreatePage (`src/pages/CreatePage.jsx`)

A dedicated page for adding new products. It validates inputs and calls the API to create a product. Success or error messages are displayed using a toast notification system.

## State Management & API

The project uses **Zustand** for simplified global state management, located in `src/store/product.js`.

### API Endpoints

The store communicates with the backend at `https://express-on-vercel-c2s.vercel.app/api/products`.

### Store Actions

- `fetchProducts()`: GET request to retrieve all products.
- `createProduct(newProduct)`: POST request. Includes validation for name, price, and image URL.
- `deleteProduct(pid)`: DELETE request to remove a product by ID.
- `updateProduct(pid, updatedProduct)`: PUT request to modify product details.

**Error Handling:** All actions return an object `{ success: boolean, message: string }` which is used by the UI components to display appropriate feedback (Toasts) to the user.

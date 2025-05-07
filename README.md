# PL.CP.MF.PORTAL

> Mounting Microfrontend for the PeraLink platform – orchestrating and managing microfrontend lifecycles.

---

## 📌 Overview

**PL.CP.MF.PORTAL** serves as the **root configuration and orchestration layer** of the PeraLink MicroFrontend (PL.MF) ecosystem. It is responsible for dynamically mounting, managing, and configuring microfrontends across the platform.

---

## ✨ Features

- **🧩 Microfrontend Integration**  
  Manages registration and lifecycle of microfrontends using [single-spa](https://single-spa.js.org/).

- **📈 Scalable Architecture**  
  Supports seamless integration of additional microfrontends without disrupting the application structure.

- **⚙️ Environment-Aware Configuration**  
  Supports different configurations for local development and public deployment using dynamic import maps.

---

## 🚀 Usage

This repository acts as the central entry point for loading and rendering other microfrontends at runtime.

---

## 🔧 Registering Microfrontends

### ✅ Local Registration

1. Open the `.ejs` template file located in the `src/` directory (e.g., `src/index.ejs`).
2. Add the following `injector-importmap` block inside the EJS logic for local development:

    ```html
    <% if (isLocal) { %>
      <script type="injector-importmap">
        {
          "imports": {
            "react": "https://cdn.jsdelivr.net/npm/react@18.0.0/+esm",
            "react-dom": "https://cdn.jsdelivr.net/npm/react-dom@18.0.0/+esm",
            "react-dom/client": "https://cdn.jsdelivr.net/npm/react-dom@18.0.0/client/+esm",
            "@peralink/root-config": "//localhost:9000/peralink-root-config.js",
            "@peralink/dashboard": "//localhost:9001/peralink-dashboard.js",
            "@peralink/core-ui": "//localhost:9002/peralink-core-ui.js",
            "@peralink/core-utility": "//localhost:9003/peralink-core-utility.js"
          }
        }
      </script>
    <% } %>
    ```

3. Run the project locally:

    ```bash
    npm start
    # or
    yarn start
    ```

4. Access the application at [http://localhost:9000](http://localhost:9000).

---

### 🌐 Public Deployment

1. In the same `src/index.ejs` file, add the following script tags for production:

    ```html
    <script src="https://cdn.jsdelivr.net/npm/import-map-overrides@5.1.1/dist/import-map-overrides.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@single-spa/import-map-injector@2.0.1/lib/import-map-injector.js"></script>
    ```

2. Ensure all remote microfrontends are:
   - Deployed and accessible via public URLs
   - Registered correctly in the public import map

3. Deploy the portal application to your hosting environment.

4. Open the deployed URL to verify all microfrontends are mounted correctly.

---

## 📝 Notes

- This repository should only handle orchestration and dynamic mounting.  
- Avoid embedding UI or business logic directly in this project.  
- Always test changes in both local and production environments.

---

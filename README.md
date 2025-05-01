# Documentation for Setting Up and Configuring Keycloak with Vue.js and Django

## Overview
This guide covers the steps required to set up and configure Keycloak for use with a Vue.js frontend and a Django backend. This includes setting up Keycloak, configuring it for PKCE (Proof Key for Code Exchange), and integrating the authentication flow in your application.

## Prerequisites
- A running instance of Keycloak.
- Vue.js project for the frontend.
- Django project for the backend.

## Keycloak Setup

### Create a Realm
1. Log in to the Keycloak admin console.
2. Click on **Add realm** and enter a name, e.g., `Vue`.

### Create a Client
1. Go to **Clients** and click **Create**.
2. Set **Client ID** to `vuejs`.
3. Set **Client Protocol** to `openid-connect`.
5. Click **Save**.

### Configure Client
#### Under the **Settings** tab:
- Set **Valid Redirect URIs** to `{BASE_URL}/*`.
- Set **Web Origins** to `+` or `{BASE_URL}`.
- Enable **Direct Access Grants** in Authentication Flow.

#### Under the **Advanced Settings** tab:
- Set **Proof Key for Code Exchange Code Challenge Method** to `S256`.

### Configure Content Security Policy
Add `frame-src 'self' {BASE_URL}; frame-ancestors 'self' {BASE_URL}; object-src 'none';` to allow iframe embedding.

## Vue.js Frontend Configuration

### Install Dependencies in Root Directory i.e frontend/
```sh
npm install
```

### Create a `.env` File

1. **Create a `.env` file**:
   - In the root directory of your Vue.js project, create a file named `.env`.

2. **Add Environment Variables**:
   - Open the `.env` file and add the following variables:
     ```plaintext
     VUE_APP_KEYCLOAK_URL={KC_BASE_URL}/auth
     VUE_APP_KEYCLOAK_REALM={REALM}
     VUE_APP_KEYCLOAK_CLIENT_ID={CLIENT_ID}
     VUE_APP_KEYCLOAK_CLIENT_SECRET={CLIENT_SECRET}
     ```

3. **Usage in Vue Project**:
   - Access these environment variables in your Vue.js project using `process.env`:
     ```javascript
     const keycloakUrl = process.env.VUE_APP_KEYCLOAK_URL;
     ```

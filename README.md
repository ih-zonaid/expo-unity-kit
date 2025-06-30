# Expo Unity Kit

Expo Unity Kit is a starter template for building full-stack, cross-platform applications where the client and server feel like a single, unified entity. Powered by Expo's API Routes, tRPC, and Turso, it eliminates the need for a separate backend server, offering a simple yet powerful, fully typesafe development experience. Get started instantly with a solid foundation, including a pre-configured Google OAuth flow.

## Features

- **UI & Styling:**
  - **NativeWind v4:** Use Tailwind CSS for styling your React Native application.
  - **Dark/Light Mode:** The application supports both dark and light themes with persistent state.
  - **Adaptive Navigation Bar:** The Android Navigation Bar color automatically matches the current theme.
- **Component Library:**
  - A set of common, reusable components built with `react-native-reusables`, providing a developer experience similar to ShadCN for React Native. Includes `ThemeToggle`, `Avatar`, `Button`, `Card`, `Progress`, `Text`, `Tooltip`, and more.
- **Full-stack Architecture:**
  - **Expo API Routes:** Leverage file-based routing for your server-side logic.
  - **tRPC:** End-to-end typesafe APIs, ensuring your frontend and backend are always in sync.
- **Authentication:**
  - Pre-configured Google OAuth flow. (Credit: [betomoedano/expo-oauth-example](https://github.com/betomoedano/expo-oauth-example))
- **Database:**
  - **Turso:** Integrated with TursoDB, a fast and lightweight edge database.
  - **Drizzle ORM:** A modern TypeScript ORM for database schema management and queries.

## Tech Stack

- **Framework:** [Expo](https://expo.dev/)
- **Styling:** [NativeWind v4](https://www.nativewind.dev/) / [Tailwind CSS](https://tailwindcss.com/)
- **API Layer:** [tRPC](https://trpc.io/) on [Expo API Routes](https://docs.expo.dev/router/reference/api-routes/)
- **Database:** [Turso](https://turso.tech/) with [Drizzle ORM](https://orm.drizzle.team/)
- **Navigation:** [React Navigation](https://reactnavigation.org/)
- **State Management:** [React Query](https://tanstack.com/query/latest)
- **UI Primitives:** [@rn-primitives](https://rn-primitives.vercel.app/)
- **Schema Validation:** [Zod](https://zod.dev/)

## Target Audience

This starter kit is perfect for developers looking to build full-stack, cross-platform applications with a modern, unified toolset. It is an excellent choice for:

- **Learning:** Understand the fundamentals of a modern Expo stack, including API Routes, tRPC, and edge databases.
- **Prototyping:** Quickly build and test new ideas with a solid, typesafe foundation.
- **Simple Applications:** Build and deploy simple, regular applications that don't require a high volume of concurrent database writes.

## Known Limitations

While this starter is robust for many use cases, it's important to be aware of a specific performance consideration for more complex scenarios:

- **Concurrent Database Writes:** In the production environment on EAS, performing a high number of simultaneous database writes (e.g., 3 or more) within a single API request can sometimes lead to errors. For most standard applications, this is not an issue, but it's a factor to consider for data-intensive features.

## Project Structure

This project uses a unified structure where client and server code coexist. Here's a brief overview of the key directories:

- **`app/`**: Contains all the client-side code, including screens, navigation, and UI components.
  - **`app/api/`**: This is where the server-side logic lives, powered by Expo API Routes. Each file in this directory becomes an API endpoint.
- **`components/`**: A collection of reusable UI components.
- **`server/`**: Contains the tRPC router, procedures, and database schema definitions.
- **`lib/`**: Shared utilities and hooks used across the application.

## Prerequisites

Before you begin, ensure you have the following installed and configured:

- **[Bun](https://bun.sh/)** (or Node.js and npm)
- **Expo CLI:** `npm install -g expo-cli`
- **Google Cloud Project:**
  - Create a new project on the [Google Cloud Console](https://console.cloud.google.com/).
  - Set up an OAuth 2.0 consent screen.
  - Create OAuth 2.0 credentials for a **Web application**. You will need the **Client ID** and **Client Secret**.
- **Turso Account:**
  - Sign up for a free [Turso](https://turso.tech/) account.
  - Install the Turso CLI: `brew install turso` (or follow the instructions for your OS).
  - Log in to your Turso account: `turso auth login`.

## Setup and Installation

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/ih-zonaid/expo-unity-kit.git
    cd expo-unity-kit
    ```

2.  **Install dependencies:**

    ```bash
    bun install
    ```

3.  **Set up environment variables:**
    Create a `.env` file by copying `.env.example` and fill in the required values:

    ```
    # Google OAuth
    GOOGLE_CLIENT_ID="your-google-client-id"
    GOOGLE_CLIENT_SECRET="your-google-client-secret"

    # Turso Database
    TURSO_DATABASE_URL="your-turso-database-url"
    TURSO_AUTH_TOKEN="your-turso-auth-token"
    ```

4.  **Set up the database:**
    - Create a new Turso database: `turso db create your-db-name`
    - Get the database URL: `turso db show your-db-name --url`
    - Get the auth token: `turso db tokens create your-db-name`
    - Push the database schema:
      ```bash
      bun run db:push
      ```

## Running the Application

- **Start the development server for all platforms:**
  ```bash
  bun run dev
  ```
- **Start for Web only:**
  ```bash
  bun run dev:web
  ```
- **Run on Android:**
  ```bash
  bun run android
  ```
- **Run on iOS:**
  ```bash
  bun run ios
  ```

## Available Scripts

- `dev`: Starts the development server for all platforms.
- `dev:web`: Starts the development server for Web only.
- `android`: Runs the app on a connected Android device or emulator.
- `ios`: Runs the app on a connected iOS device or simulator.
- `db:push`: Pushes your Drizzle schema changes to the database.
- `db:generate`: Generates Drizzle migration files.
- `web:build`: Creates a production build for the web.
- `web:deploy`: Deploys the web build using EAS Deploy.
- `clean`: Removes `node_modules` and `.expo` for a clean reinstall.

## Authentication Flow

This starter includes a complete Google OAuth 2.0 flow. The authentication logic is handled server-side via Expo API Routes located in `app/api/auth/`. The client-side code uses an `AuthContext` to manage the user's session and protect routes.

## Deployment

This project is configured for deployment using EAS (Expo Application Services).

### Web Deployment

You can deploy the web version of this application directly from the command line.

1.  **Ensure you are logged into your Expo account:**
    ```bash
    eas login
    ```
2.  **Deploy to EAS:**
    ```bash
    bun run web:deploy
    ```
    This command will build and deploy your web app to Expo's hosting service.

## Contributing

Contributions are welcome! Please feel free to open an issue or submit a pull request.

## License

This project is licensed under the MIT License.

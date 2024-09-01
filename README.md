# Ultimate Starter Pack

## Overview

This starter pack is designed to accelerate the development of modern web applications by providing a robust foundation. It includes a comprehensive setup with Next.js, TypeScript, Hasura, Auth0, Express, Husky, Jest, Prettier, and more. The pack is pre-configured with industry-standard tools and workflows, ensuring a smooth development experience, and what truly sets it apart is how it enables you to get an industry-standard CI/CD pipeline, leveraging NEONDB’s database branching, up and running in just 5 minutes.

---

## Developer Experience

- **Next.js & TypeScript 🖥️📜**: Build scalable and maintainable frontend applications with TypeScript support.
- **Express.js 🌐**: A well-structured backend with Helmet for security and Morgan for logging.
- **Hasura ⚡**: Integrated GraphQL engine for instant backend with PostgreSQL.
- **Auth0 🔐**: Authentication and authorization with Auth0, configured for secure and easy user management.
- **Prisma & NeonDB 🗄️🚀**: Database ORM with Prisma, optimized for NeonDB, and CI/CD workflows via GitHub Actions.
- **Vercel 🚀**: Seamless deployment with Vercel, pre-configured for Next.js applications.
- **Jest 🧪**: Testing framework with a complete setup for both frontend and backend.
- **Husky & Prettier 🐕🎨**: Pre-commit hooks with Husky and code formatting with Prettier for consistent code quality.
- **Nodemon 🔄**: Live reload with Nodemon, configured for TypeScript to automatically restart the server on changes.
- **Initialization Script ⚙️**: Automated setup script to remove the original GitHub repository, initialize a new one, and push it to a newly created GitHub repository via the GitHub API.

### Prerequisites

- **Node.js 16+** and **npm**
- **GitHub Token**: A GitHub token with repository access.
- **Vercel Token**: A Vercel token for deployment.
- **NeonDB Credentials**: API key, connection string, and pooled connection string.
- **Auth0 Credentials**: Domain, Client ID, and Client Secret.
- **Hasura Credentials**: Admin Secret.
  The 'Getting Credentials' section provides detailed instructions on how to obtain all the necessary credentials.

### Getting Started

1. **Clone the Repository**:

   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. **Install Dependencies**:

   ```bash
   npm install
   ```

3. **Run the Initialization Script**:

   ```bash
   npm run init-project
   ```

   This script will:

   - Remove the existing `.git` directory.
   - Initialize a new Git repository.
   - Create a new repository on GitHub using the GitHub API.
   - Setup Action Secrets on GitHub using the GitHub API.
   - Set up environment variables in a `.env` file.
   - Push the initial commit to the newly created GitHub repository.

4. **Run the Application**:
   ```bash
   npm run dev
   ```
   This command will start both the Next.js frontend and the Express.js backend, as well as initiate the Hasura Docker container. You can access the services at the following addresses:
   - Next.js frontend: [http://localhost:3000](http://localhost:3000)
   - Express.js backend: [http://localhost:4000](http://localhost:4000)
   - Hasura Docker container: [http://localhost:8081](http://localhost:8080)

### CI/CD Workflow

- **Clean Up Preview Deployment (`cleanup-preview.yml`):**
  - Triggered when a pull request is closed.
  - Deletes the associated Neon branch using the `neondatabase/delete-branch-action` to clean up resources.
- **Deploy Preview (`deploy-preview.yml`):**
  - Triggered on pull requests.
  - Checks out the code.
  - Retrieves the branch name.
  - Creates a Neon database branch for the preview environment.
  - Runs Prisma migrations to set up the Neon database schema.
  - Installs the Vercel CLI.
  - Pulls Vercel environment information and builds the project artifacts.
  - Deploys the preview build to Vercel.
  - Comments on the pull request with links to the Vercel preview URL and Neon branch.
- **Deploy Production (`deploy-production.yml`):**
  - Triggered on pushes to the main branch.
  - Checks out the code.
  - Runs Prisma migrations for the production Neon database.
  - Installs the Vercel CLI.
  - Pulls Vercel environment information and builds the production project artifacts.
  - Deploys the production build to Vercel.

## Project Structure

```
├── .github
│   └── workflows
│       ├── cleanup-preview.yml   # GitHub Actions workflow for cleaning up preview environments
│       ├── deploy-preview.yml     # GitHub Actions workflow for deploying preview environments
│       └── deploy-production.yml  # GitHub Actions workflow for deploying production
├── .env                        # Environment variables
├── .eslintignore               # ESLint ignore rules
├── .eslintrc.json              # ESLint configuration
├── .gitignore                  # Git ignore rules
├── .husky
│   ├── husky.sh                # Husky setup script
│   └── pre-commit              # Pre-commit hook
├── .prettierignore             # Prettier ignore rules
├── .prettierrc                 # Prettier configuration
├── .vscode
│   ├── extensions.json         # VSCode extensions recommendations
│   └── settings.json           # VSCode settings
├── README.md                   # Project documentation
├── docker-compose.yml          # Docker Compose configuration for Hasura
├── eslint.config.mjs           # ESLint configuration
├── jest.config.js              # Jest configuration
├── next-env.d.ts               # TypeScript environment definitions for Next.js
├── next.config.js              # Next.js configuration
├── package.json                # NPM scripts and dependencies
├── package-lock.json           # NPM lockfile
├── postcss.config.js           # PostCSS configuration
├── public
│   ├── favicon.ico             # Favicon
│   ├── next.svg                # Next.js logo
│   └── vercel.svg              # Vercel logo
├── prisma
│   └── schema.prisma           # Prisma schema
├── pages
│   ├── _app.tsx                # Custom App component for Next.js
│   ├── _document.tsx           # Custom Document component for Next.js
│   ├── api
│   │   ├── auth
│   │   │   └── [auth0].ts      # Auth API route
│   │   └── hello.ts            # Hello API route
│   └── index.tsx               # Main entry point for Next.js pages
├── quickstart.js               # Quickstart script
├── server
│   ├── __tests__
│   │   └── app.test.ts         # Application mock tests
│   ├── app.ts                  # Main server application
│   ├── routes.ts               # API routes
│   └── tsconfig.json           # TypeScript configuration for server
├── styles
│   └── globals.css             # Global CSS styles
├── tailwind.config.js          # Tailwind CSS configuration
└── tsconfig.json               # TypeScript configuration

```

## Getting Credentials

### **Neon**

![[NEON1NEON.png]]

1. Head over to Neon to sign up for a free account.

---

![[NEON2NEON.png]]

2. Give your Neon project a name.
3. Click on the **Create Project** button.

---

![[NEON4NEON.png]]

Click on **Dashboard**. 4. Copy your direct PostgreSQL connection string. 5. Tick the **Pooled connection** checkbox to copy the pooled connection string.

---

![[NEON5NEON.png]]

6. Click on **Overview**.
7. Copy your Project ID.
8. Click on your avatar.
9. Click on **Account Settings**.

---

![[NEON6NEON.png]]

10. Click on **API Keys**.
11. Click on **Create new API Key**.
    - Name your API key.
12. Finally, click on **Create** and copy your Neon API Key.

---

### **Auth0**

![[AUTH1AUTH0.png]]

0. Head over to Auth0 to sign up.

---

![[AUTH2AUTH0.png]]

1. Click on **I have used Auth0 before**.

---

![[AUTH3AUTH0.png]]

2. Click on the **Create Application** button.

---

![[AUTH4AUTH0.png]]

3. Give your application a name.
4. Click on **Regular Web Applications**.
5. Click on **Create**.

---

![[AUTH5AUTH0.png]]

6. Click on **Next.js**.

---

![[AUTH6AUTH0.png]]

7. Copy the **Domain**.
8. Copy your **Client ID**.
9. Copy your **Client Secret**.

---

![[AUTH7AUTH0.png]]

10. Set your **Allowed Callback URLs** to `http://localhost:3000/api/auth/callback`.
11. Set **Logout URLs** to `http://localhost:3000`.
12. Click on **Save Changes**.

---

### **GitHub**

![[GH1GH.png]]

0. Head over to your [GitHub Settings](https://github.com/settings/tokens).
1. Click on **Tokens (classic)**.
2. Click on **Generate new token**.
3. Select **Generate new token (classic)**.

---

![[GH2GH.png]]

4. Give your token a name.
5. Set an expiration date (a short expiration is fine since the token will be used just once by the initialization script).
6. Tick **repo** to authorize the initialization script to create your repo and populate the required Action Secrets.

---

![[GH3GH.png]]

7. Click on **Generate token** and copy your token.

---

### **Vercel**

![[VERCEL1VERCEL.png]]

0. Head to [Vercel](https://vercel.com).

---

![[VERCEL2VERCEL.png]]

1. Click on your avatar.
2. Click on **Account Settings**.

---

![[VERCEL3VERCEL.png]]

3. Click on **Tokens** in the left menu bar.
4. Click on **Create**, give your token a name.
5. Copy your token.

---

### **Hasura**

![[Hasura1Hasura.png]]

0. Head over to [Hasura](https://hasura.io) and create a new account.

---

![[Hasura2Hasura.png]]

1. Click on **Create a project**.

---

![[Hasura3Hasura.png]]

2. Click on **Create Free Project**.

---

![[Hasura4Hasura.png]]

3. Copy your **Admin Secret**.

## Contributing

Contributions are welcome! Please submit a pull request or open an issue to discuss your ideas.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [Next.js](https://nextjs.org/)
- [TypeScript](https://www.typescriptlang.org/)
- [Hasura](https://hasura.io/)
- [Auth0](https://auth0.com/)
- [Prisma](https://www.prisma.io/)
- [NeonDB](https://neon.tech/)
- [Vercel](https://vercel.com/)
- [GitHub Actions](https://github.com/features/actions)

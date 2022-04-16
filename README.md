# Fullstack Authentication Example with Next.js, NextAuth.js, and PostgreSQL.

This is a basic blog project for the fullstack tutorial with Next.js and Prisma.

## Languages

- HTML5
- Tailwind CSS
- NextJs
- React
- Typescript
- Prisma
- PostgreSQL

## Getting Started

1. Run `npm install` to install the required dev dependencies.

2. I have used a custom port, so run your server with `npm run dev -- -p 3300`.
   You can change to a port number of your choice by changing `"dev:" "next dev -p [your_port_number]"` the in the `package.json` file.

3. Open [http://localhost:3300](http://localhost:3300) with your browser to see the result.

4. You can start editing the page by modifying `pages/index.js`. The page auto-updates as you edit the file.

# Prisma Setup

1. Run `npx prisma init` to create your prisma schema in the prisma directory.

2. Set the `DATABASE_URL` in the `.env` file to point to your existing database. If your database has no tables yet, read [Getting started](https://pris.ly/d/getting-started).

3. Set the `provider` of the `datasource` block in `schema.prisma` to match `postgresql` database.

4. Run `npx prisma db push` to create the tables in your database.

5. `npx prisma studio` to use Prisma Studio's interface amd create a new `User` and `Post` record and connect them via their relation fields.

6. Because Prisma Client is tailored to your own schema, you need to update it every time your Prisma schema file is changing by running the following command: `npx prisma generate`.

7. You'll use a single `PrismaClient` instance that you can import into any file where it's needed. The instance will be created in a `prisma.ts` file inside the `lib/` directory. Go ahead and create the missing directory and file: `mkdir lib && touch lib/prisma.ts`

8. Add the following code in the `prisma.ts` file:
<pre><code>
import { PrismaClient } from "@prisma/client";

let prisma: PrismaClient;

if (process.env.NODE_ENV === "production") {
prisma = new PrismaClient();
} else {
if (!global.prisma) {
global.prisma = new PrismaClient();
}
prisma = global.prisma;
}

export default prisma;
</code></pre>

# Github Authentication Setup

Just in case you need to setup your own authentication in a different project

1. Install the `NextAuth.js` library in your app: `npm install next-auth@4 @next-auth/prisma-adapter`

2. For this project I created 3 more models `Account`, `Session`, and `VerificationToken` in the `schema.prisma` file.

3. Run the `npx prisma db push` command again.

4. Since you're using GitHub authentication, you also need to create a new [OAuth app on GitHub](https://docs.github.com/en/free-pro-team@latest/developers/apps/building-oauth-apps). First, log into your [GitHub](https://github.com/) account. Then, navigate to
   [Settings](https://github.com/settings/profile), then open to
   [Developer Settings](https://github.com/settings/apps), then switch to
   [OAuth Apps](https://github.com/settings/developers).

5. Clicking on the Register a new application (or New OAuth App) button will redirect you to a registration form to fill out some information for your app. The Authorization callback URL should be the Next.js `/api/auth` route: `http://localhost:3300/api/auth`.
   `
6. Add your keys for GitHub Authentication in your `.env` file.

```
  GITHUB_ID=[your_id]
  GITHUB_SECRET=[you_secret_key]
  NEXTAUTH_URL=http://localhost:3300/api/auth
```

# Extra
For a full tutorial on developing a Full Stack Application: [How to build a full-stack app with NextJs, Prisma and PostgreSQL](https://vercel.com/guides/nextjs-prisma-postgres)

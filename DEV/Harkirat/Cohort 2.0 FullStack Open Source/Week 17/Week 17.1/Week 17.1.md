# Building Paytm (1/3)

Up until now, our discussions have primarily revolved around theoretical concepts. In this lecture, Harkirat takes a `practical approach` by guiding us through the hands-on process of `building a Paytm like application`

  

The stack for this project includes Next.js for the frontend and backend (or a separate backend), Express for auxiliary backends, Turborepo for managing the monorepo, a PostgreSQL database, Prisma as the ORM, and Tailwind for styling.

  

> While there are `no specific notes` provided for this section, a mini guide is outlined below to assist you in navigating through the process of building the application. Therefore, it is strongly `advised to actively follow along` during the lecture for a hands-on learning experience.

  

Building Paytm (1/3)

Introduction

Feature planning

User login

Merchant login

UI/UX (End User)

Login

Landing Page

User Home Page

User Transfer Page

UI/UX (Merchant)

Architecture

Hot paths

This is ~1 month job for a 2 engineer team.

Stack

Bootstrap the app

Adding prisma

Add a recoil/store module

Import recoil in the next.js apps

Add next-auth

Database

User-app

Merchant-app

Add auth

Client side

Server side

Add an Appbar component

Checkpoint

  

![Untitled 33.png](../../../../Images/Untitled%2033.png)

  

# Introduction

In this hands-on lecture, we will be building a Paytm-like application. The first step is to plan the features and design the user interface (UI) and user experience (UX). For the UX, we can either follow first principles or take inspiration from existing successful websites. As for the UI, while there are tools available, finding a good one can be challenging.

  

Next, we will focus on the high-level design, including the authentication provider, database, backend stack, frontend stack, and the modules we'll have (such as common, UI, and backend). We'll also decide on the cloud platform for deployment. Additionally, we'll delve into the low-level design, including schema design, route signatures, and frontend components. While entity-relationship diagrams can be useful, they may not be necessary unless you're a highly visual person.

  

# **Feature planning**

### **User login**

1. Auth (In this case, probably email/phone)  
2. On ramp from bank, off ramp to bank  
3. Support transfers via phone number/name  
4. Support scanning a QR code for transferring to merchants  

### **Merchant login**

1. Login with google  
2. Generate a QR Code for acceptance  
3. Merchants get an alert/notification on payment  
4. Merchant gets money offramped to bank every 2 days  

  

  

# **UI/UX (End User)**

### **Login**

![Untitled 1 26.png](../../../../Images/Untitled%201%2026.png)

  

![Untitled 2 18.png](../../../../Images/Untitled%202%2018.png)

  

### Landing Page

![Untitled 3 15.png](../../../../Images/Untitled%203%2015.png)

  

### User Home Page

![Untitled 4 13.png](../../../../Images/Untitled%204%2013.png)

  

  

### User Transfer Page

![Untitled 5 11.png](../../../../Images/Untitled%205%2011.png)

  

![Untitled 6 10.png](../../../../Images/Untitled%206%2010.png)

  

  

![Untitled 7 9.png](../../../../Images/Untitled%207%209.png)

  

  

# **UI/UX (Merchant)**

![Untitled 8 8.png](../../../../Images/Untitled%208%208.png)

  

![Untitled 9 7.png](../../../../Images/Untitled%209%207.png)

  

![Untitled 10 7.png](../../../../Images/Untitled%2010%207.png)

  

# **Architecture**

  

![Untitled 11 5.png](../../../../Images/Untitled%2011%205.png)

[![](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F085e8ad8-528e-47d7-8922-a23dc4016453%2F888fec18-4140-4f67-9820-7878a4897e84%2FScreenshot_2024-03-23_at_6.35.20_PM.png?table=block&id=c791d5db-4676-4d03-b8e6-587f9854dab5&cache=v2)](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F085e8ad8-528e-47d7-8922-a23dc4016453%2F888fec18-4140-4f67-9820-7878a4897e84%2FScreenshot_2024-03-23_at_6.35.20_PM.png?table=block&id=c791d5db-4676-4d03-b8e6-587f9854dab5&cache=v2)

### **Hot paths**

1. Send money to someone
2. Withdraw balance of merchant
3. Withdraw balance of user back to bank
4. Webhooks from banks to transfer in money

### **This is ~1 month job for a 2 engineer team.**

We can cut scope in either

1. UI
2. Number of features we support (remove merchant altogether)
3. Number of services we need (merge bank server, do withdrawals directly and not in a queue assuming banks are always up)

  

# **Stack**

1. Frontend and Backend - Next.js (or Backend)  
2. Express - Auxilary backends  
3. Turborepo  
4. Postgres Database  
5. Prisma ORM  
6. Tailwind  

  

  

# **Bootstrap the app**

- Init turborepo

```Shell
 npx create-turbo@latest
```

- Rename the two Next apps to
    1. user-app
    2. merchant-app
- Add tailwind to it.

```Shell
cd apps/user-app
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

cd ../merchant-app
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

  

> [!important]  
> You can also use https://github.com/vercel/turbo/tree/main/examples/with-tailwind  

Update `tailwind.config.js`

```JavaScript

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./app/**/*.{js,ts,jsx,tsx,mdx}",
    "./pages/**/*.{js,ts,jsx,tsx,mdx}",
    "./components/**/*.{js,ts,jsx,tsx,mdx}",
    "../../packages/ui/**/*.{js,ts,jsx,tsx,mdx}"
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Update `global.css`

```JavaScript

@tailwind base;
@tailwind components;
@tailwind utilities;
```

  

> [!important]  
> Ensure tailwind is working as expected  

  

  

# **Adding prisma**

Ref - [https://turbo.build/repo/docs/handbook/tools/prisma](https://turbo.build/repo/docs/handbook/tools/prisma)

1. Create a new `db` folder
2. Initialise package.json

```Shell
npm init -y
npx tsc --init
```

1. Update package.json

```JavaScript

{
    "name": "@repo/db",
    "version": "0.0.0",
    "dependencies": {
        "@prisma/client": "^5.11.0"
    },
    "devDependencies": {
        "prisma": "5.11.0"
    },
    "exports": {
        "./client": "./index.ts"
    }
}
```

1. Update tsconfig.json

```JavaScript

{
    "extends": "@repo/typescript-config/react-library.json",
    "compilerOptions": {
      "outDir": "dist"
    },
    "include": ["src"],
    "exclude": ["node_modules", "dist"]
  }
```

1. Init prisma

```JavaScript
npx prisma init
```

1. Start DB locally/on neon.db/on aiven
2. Update .env with the new database URL
3. Add a basic schema

```JavaScript
model User {
  id    Int     @id @default(autoincrement())
  email String  @unique
  name  String?
}
```

1. MIgrate DB

```JavaScript
npx prisma migrate
```

1. Update `index.ts`

```JavaScript
export * from '@prisma/client';
```

1. Try adding `api/user/route.ts`

```JavaScript
import { NextResponse } from "next/server"
import { PrismaClient } from "@repo/db/client";

const client = new PrismaClient();

export const GET = async () => {
    await client.user.create({
        data: {
            email: "asd",
            name: "adsads"
        }
    })
    return NextResponse.json({
        message: "hi there"
    })
}
```

  

  

# **Add a recoil/store module**

- Create `store` package

```Shell
cd packages
mkdir store
npm init -y
npx tsc --init
```

- Install dependencies

```Shell
npm i recoil
```

- Update tsconfig.json

```JavaScript
{
    "extends": "@repo/typescript-config/react-library.json",
    "compilerOptions": {
      "outDir": "dist"
    },
    "include": ["src"],
    "exclude": ["node_modules", "dist"]
}
```

- Update package.json

```JavaScript
{
  "name": "@repo/store",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "recoil": "^0.7.7"
  }
}
```

- Create a simple `atom` called balance in `src/atoms/balance.ts`

```JavaScript
import { atom } from "recoil";

export const balanceAtom = atom<number>({
    key: "balance",
    default: 0,
})
```

- Create a simple `hook` called `src/hooks/useBalance.ts`

```JavaScript
import { useRecoilValue } from "recoil"
import { balanceAtom } from "../atoms/balance"

export const useBalance = () => {
    const value = useRecoilValue(balanceAtom);
    return value;
}
```

- Add export to package.json

```TypeScript
"exports": {
    "./useBalance": "./src/hooks/useBalance"
}
```

  

  

# **Import recoil in the next.js apps**

- Install recoil in them

```Shell
npm i recoil
```

- Add a `providers.tsx` file

```JavaScript
"use client"
import { RecoilRoot } from "recoil";

export const Providers = ({children}: {children: React.ReactNode}) => {
    return <RecoilRoot>
        {children}
    </RecoilRoot>
}
```

- Update `layout.tsx`

```JavaScript

 return (
    <html lang="en">
      <Providers>
        <body className={inter.className}>{children}</body>
      </Providers>
    </html>
  );
```

- Create a simple client component and try using the `useBalance` hook in there

```JavaScript
"use client";

import { useBalance } from "@repo/store/useBalance";

export default function() {
  const balance = useBalance();
  return <div>
    hi there {balance}
  </div>
}
```

If you see this, we’ll try to debug it end of class. Should still work in dev mode

![Untitled 12 4.png](../../../../Images/Untitled%2012%204.png)

  

  

# **Add next-auth**

### **Database**

Update the database schema

```JavaScript
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id          Int      @id @default(autoincrement())
  email       String?  @unique
  name        String?
  number      String  @unique
  password    String
}

model Merchant {
  id          Int     @id @default(autoincrement())
  email       String  @unique
  name        String?
  auth_type   AuthType
}

enum AuthType {
  Google
  Github
}
```

### **User-app**

- Go to `apps/user-app`
- Initialize next-auth

```Shell
npm install next-auth
```

- Initialize a simple next auth config in `lib/auth.ts`

```JavaScript
import db from "@repo/db/client";
import CredentialsProvider from "next-auth/providers/credentials"
import bcrypt from "bcrypt";

export const authOptions = {
    providers: [
      CredentialsProvider({
          name: 'Credentials',
          credentials: {
            phone: { label: "Phone number", type: "text", placeholder: "1231231231" },
            password: { label: "Password", type: "password" }
          },
          // TODO: User credentials type from next-aut
          async authorize(credentials: any) {
            // Do zod validation, OTP validation here
            const hashedPassword = await bcrypt.hash(credentials.password, 10);
            const existingUser = await db.user.findFirst({
                where: {
                    number: credentials.phone
                }
            });

            if (existingUser) {
                const passwordValidation = await bcrypt.compare(credentials.password, existingUser.password);
                if (passwordValidation) {
                    return {
                        id: existingUser.id.toString(),
                        name: existingUser.name,
                        email: existingUser.number
                    }
                }
                return null;
            }

            try {
                const user = await db.user.create({
                    data: {
                        number: credentials.phone,
                        password: hashedPassword
                    }
                });

                return {
                    id: user.id.toString(),
                    name: user.name,
                    email: user.number
                }
            } catch(e) {
                console.error(e);
            }

            return null
          },
        })
    ],
    secret: process.env.JWT_SECRET || "secret",
    callbacks: {
        // TODO: can u fix the type here? Using any is bad
        async session({ token, session }: any) {
            session.user.id = token.sub

            return session
        }
    }
  }
```

- Create a `/api/auth/[...nextauth]/route.ts`

```JavaScript
import NextAuth from "next-auth"

const handler = NextAuth(authOptions)

export { handler as GET, handler as POST }
```

- Update .env

```Shell
JWT_SECRET=test
NEXTAUTH_URL=http://localhost:3001
```

- Ensure u see a signin page at [http://localhost:3000/api/auth/signin](http://localhost:3000/api/auth/signin)

### **Merchant-app**

Create `lib/auth.ts`

```JavaScript
import GoogleProvider from "next-auth/providers/google";

export const authOptions = {
    providers: [
        GoogleProvider({
            clientId: process.env.GOOGLE_CLIENT_ID || "",
            clientSecret: process.env.GOOGLE_CLIENT_SECRET || ""
        })
    ],
  }
```

- Create a `/api/auth/[...nextauth]/route.ts`

```JavaScript
import NextAuth from "next-auth"

const handler = NextAuth(authOptions)

export { handler as GET, handler as POST }
```

- Put your google client and secret in `.env` of the merchant app.  
    Ref  
    [https://next-auth.js.org/providers/google](https://next-auth.js.org/providers/google)

```JavaScript
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=kiratsecr3t
```

- Ensure u see a signin page at [http://localhost:3001/api/auth/signin](http://localhost:3001/api/auth/signin)
- Try signing in and make sure it reaches the DB

  

  

# **Add auth**

### **Client side**

- Wrap the apps around `SessionProvider` context from the next-auth package
- Go to `merchant-app/providers.tsx`

```JavaScript
"use client"
import { RecoilRoot } from "recoil";
import { SessionProvider } from "next-auth/react";

export const Providers = ({children}: {children: React.ReactNode}) => {
    return <RecoilRoot>
        <SessionProvider>
            {children}
        </SessionProvider>
    </RecoilRoot>
}
```

- Do the same for `user-app/providers.tsx`

### **Server side**

Create `apps/user-app/app/api/user.route.ts`

```JavaScript
import { getServerSession } from "next-auth"
import { NextResponse } from "next/server";
import { authOptions } from "../../lib/auth";

export const GET = async () => {
    const session = await getServerSession(authOptions);
    if (session.user) {
        return NextResponse.json({
            user: session.user
        })
    }
    return NextResponse.json({
        message: "You are not logged in"
    }, {
        status: 403
    })
}
```

Ensure login works as exptected

  

# **Add an Appbar component**

- Update the `Button` component in UI

```JavaScript
"use client";

import { ReactNode } from "react";

interface ButtonProps {
  children: ReactNode;
  onClick: () => void;
}

export const Button = ({ onClick, children }: ButtonProps) => {
  return (
    <button onClick={onClick} type="button" className="text-white bg-gray-800 hover:bg-gray-900 focus:outline-none focus:ring-4 focus:ring-gray-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2">
      {children}
    </button>

  );
};
```

- Create a `ui/Appbar` component that is highly generic (doesnt know anything about the user/how to logout).

```JavaScript
import { Button } from "./button";

interface AppbarProps {
    user?: {
        name?: string | null;
    },
    // TODO: can u figure out what the type should be here?
    onSignin: any,
    onSignout: any
}

export const Appbar = ({
    user,
    onSignin,
    onSignout
}: AppbarProps) => {
    return <div className="flex justify-between border-b px-4">
        <div className="text-lg flex flex-col justify-center">
            PayTM
        </div>
        <div className="flex flex-col justify-center pt-2">
            <Button onClick={user ? onSignout : onSignin}>{user ? "Logout" : "Login"}</Button>
        </div>
    </div>
}
```

  

# **Checkpoint**

We are here - [https://github.com/100xdevs-cohort-2/paytm-project-starter-monorepo](https://github.com/100xdevs-cohort-2/paytm-project-starter-monorepo)
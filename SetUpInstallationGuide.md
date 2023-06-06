## Basic Setup Guide:

### requirements:

- Node JS installed
- DB installed locally or an a server (I used POSTGRESQL locally)
- Reccomended install Prisma VSCode extension

### dependencies:

- npm init -y

```
npm install --save-dev prisma typescript ts-node @types/node nodemon @prisma/client
```

### Steps

Update tsconfig.json

Check prisma documentation, or use your projects.
sample used on project is here:

```
{
  "compilerOptions": {
    "sourceMap": true,
    "outDir": "dist",
    "strict": true,
    "lib": ["ESNext"],
    "esModuleInterop": true
  }
}
```

### Initialize Prisma

- Run below command to generate the prisma files

```
npx prisma init --datasource-provider postgresql
```

- update the .env file with the database URL
- You need to set up and run a local instance of POSTGRESQL and copy and paste the URL in there with username and password. See sample below:

```
DATABASE_URL="postgresql://postgres:password@localhost:5432/test"
```

## Creating our models and saving models to DB

- at this stage we will create our DB models
- dev = telling prisma we are in developement
- init = the name we have given it

```
npx prisma migrate dev init
```

- the above generates the client
- if we modify our models then we need to regenerate our client with

```
npx prisma generate
```

## interacting with the database

- We paste the prisma client into a new file in this case our script.ts
- for development we used nodemon and the script to speed up dev in our package.json

```
  "devStart": "nodemon script.ts"
```

- We can then write the following boilerplate
- The disconnect is optional, but a good practice to follow

```
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

async function main() {
await prisma.user.XXXXXX

* all our code is done here *
}

main()
  .catch((e) => console.error(e.message))
  .finally(async () => {
    await prisma.$disconnect();
  });
```

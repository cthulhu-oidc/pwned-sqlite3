# pwned-sqlite3
Use a local sqlite3 db for checking if a password is pwned.

# System requirements

You must be using Node.js v10.20.1 or above for better-sqlite3. Prebuilt binaries for better-sqlite3 are available for [LTS versions](https://nodejs.org/en/about/releases/).
You need about 15,4 GBy free space for the sqlite3 database (haveIBeenPwned password list version 7).

# Build your database

Download the SHA-1 password list (tested with "Version 7 (ordered by hash)" from [Have I Been Pwned](https://haveibeenpwned.com/Passwords).

Use build_database.py (see github-repo) to build the database. Modify if necessary the variables `path` and `dbName`. Python is about 30x faster than an equivalent solution in node.

The Version 7 Database is about 15.4 GBy big. 

# Performance

On my Ryzen 7 4800H and 64 GB RAM it needs about 450 ms for 100.000 runs. 

# Code Snippet

```typescript
import { join } from "path";
import { pwned, connect } from "pwned-sqlite3";

connect(join(__dirname, "pwned.sqlite3"));

function isPwned(value: string) {
    return (pwned(value));
}
```

# Avoiding Supply Chain Attacks

I activated 2FA for npmjs. But you could also just copy the code directly into your project and never worry about a possible tainted package, as the package is actually pretty simple. 

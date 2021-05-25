This repository contains unofficial patterns, sample code, or tools to help developers build more effectively with [Fauna][fauna]. All [Fauna Labs][fauna-labs] repositories are provided “as-is” and without support. By using this repository or its contents, you agree that this repository may never be officially supported and moved to the [Fauna organization][fauna-organization].

---
# Learn With Jason

This repository contains the sample code from the 25 May 2021 episode of [Learn With Jason][episode], "User-defined functions in Fauna." The code provides increasingly complex and realistic examples of [user-defined functions][udfs] (UDFs) implemented in the [Fauna Query Language][fql] (FQL) using the [Fauna Schema Migrate][fauna-schema-migrate] (FSM) tool.

## Using this repository

You can deploy the functions in this repository into your own account using either the [Fauna dashboard][fauna-dashboard] or FSM. Both instructions assume you have already created a database in the Fauna dashboard.

**Note**: Be sure to check *Pre-populate with demo data* when creating your database!

### Using the Fauna dashboard

Open the Fauna dashboard and select the *Shell* tab. Copy the code of the function you wish to deploy, paste it into the code editor, and choose the *Run Query* button. Fauna runs the *CreateFunction* statement and adds the function to your database. You can confirm this by selecting the *Functions* tab.

To run your function, copy the sample function call from the function definition file, return to the *Shell* tab, and paste the function call into the code editor. Be sure to remove any leading slashes `//`, then choose the *Run Query* button. Fauna invokes your function and displays the results.

### Using FSM

1. In the Fauna dashboard, select the *Security* tab and choose *New Key*. Accept the defaults and choose *Save* to generate a new key. Copy this key to use in the next step.
1. Set the environment variable *FAUNA_ADMIN_KEY* to the value of the key you copied in the previous step. **Note**: Be sure to add a space before `export` to avoid storing the key in your shell history.
    ```bash
     export FAUNA_ADMIN_KEY=<secret-key>
    ```
1. Clone this repository and install dependencies with `npm install`.
1. Generate a migration using FSM by running `npx fauna-schema-migrate generate`.
1. Apply the migration using FSM by running `npx fauna-schem-migrate apply`.

This defines all of the UDFs in the database where you created the key. Call these functions using the same steps outlined previously in the section [Using the Fauna dashboard](#using-the-fauna-dashboard).

## Order of progress

To learn more about UDFs in Fauna, visit the sample functions in the following order. Each file contains the function definition and samples for invoking the function in the Fauna dashboard.

1. [Hello world](resources/functions/hello-world.fql) - The classic "Hello, world!" function implemented in FQL! Start here to learn the syntax for defining and invoking UDFs. Accepts a single variable, concatenates some strings, and returns the result.
1. [Limited sum](resources/functions/limit-adder.fql) - Double the parameters but far more functionality! Demonstrates multiple parameters, branch with [`If`][fql-if], and throwing errors with [`Abort`][fql-abort].
1. [Gated primitives](resources/functions/gated-primitive.fql) - Demonstrates wrapping FQL functionality, which is useful for restricting privileges, performing attribute-based authentication control (ABAC), unit testing your UDFs, and injecting failures. Also introduces function roles, which allow the UDF to run with permissions different from the invoking user or resource.

    **WARNING**: Do not use this function in production - it does not properly handle results!

1. [Reduced primitives](resources/functions/reduced-primitive.fql) - Refines the `gated-primitive` function to return results and handle errors.

---

Copyright Fauna, Inc. or its affiliates. All rights reserved. SPDX-License-Identifier: MIT-0

[episode]: https://www.learnwithjason.dev/user-defined-functions-in-fauna
[fauna]: https://www.fauna.com/
[fauna-labs]: https://github.com/fauna-labs
[fauna-organization]: https://github.com/fauna
[fauna-schema-migrate]: https://github.com/fauna-labs/fauna-schema-migrate/
[fql]: https://docs.fauna.com/fauna/current/api/fql/
[fql-abort]: https://docs.fauna.com/fauna/current/api/fql/functions/abort
[fql-if]: https://docs.fauna.com/fauna/current/api/fql/functions/if
[udfs]: https://docs.fauna.com/fauna/current/tutorials/basics/functions

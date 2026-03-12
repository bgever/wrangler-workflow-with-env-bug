# wrangler-workflow-with-env-bug
Reproduction of local environment worker to workflow connection bug with wrangler

## Setup

`npm create cloudflare@latest workflows-starter -- --template "cloudflare/workflows-starter"`
`npm create cloudflare@latest -- my-first-worker` -> Hello World example -> Worker only.

## Reproduction steps

1. Run `npm i` in both `workflows-starter/` and `my-first-worker/`.
2. From `workflows-starter/` run `npm start`.
3. From `my-first-worker/` run `npm start`.  
   The following error should appear in the console output of my-first-worker:  
   ```text
   ✘ [ERROR] Worker "workflows:workflows-starter"'s binding "USER_WORKFLOW" refers to a service "core:user:workflows-starter", but no such service is defined.

   ✘ [ERROR] The Workers runtime failed to start. There is likely additional logging output above.
   ```
4. Stop both instances.
5. From `my-first-worker/` run `npm run start:both`.  
   Both workers should start normally.
6. Stop the instance.
7. From `my-first-worker/` run `npm run start:both:local`.  
   Both workers should start normally, but note the `-local` suffix in their reported names.

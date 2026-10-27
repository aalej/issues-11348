# Repro for issue 11348

## Versions

firebase-tools: v15.34.1

## Steps to reproduce

1. Run `firebase deploy --only dataconnect --project PROJECT_ID`

```
$ firebase deploy --only dataconnect --project PROJECT_ID

=== Deploying to 'PROJECT_ID'...

i  deploying dataconnect
i  dataconnect: ensuring required API firebasedataconnect.googleapis.com is enabled...
i  dataconnect: ensuring required API sqladmin.googleapis.com is enabled...
i  dataconnect: Successfully compiled schema and connectors
i  dataconnect: Checking for CloudSQL resources...
i  dataconnect: Found existing Cloud SQL instance test-iid.
i  dataconnect: Found existing Postgres Database secure-db.
✔  dataconnect: Deployed connector projects/PROJECT_ID/locations/us-central1/services/test-dc-2/connectors/default
i  dataconnect: Generating SQL schema migrations to be compatible...
✔  dataconnect: Database schema of test-iid:secure-db is compatible with SQL Connect Schema.
✔  dataconnect: Migrated schema projects/PROJECT_ID/locations/us-central1/services/test-dc-2/schemas/main
✔  dataconnect: Deployment complete! View your deployed schema and connectors at

    https://console.firebase.google.com/project/PROJECT_ID/dataconnect/locations/us-central1/services/test-dc-2/schema


✔  Deploy complete!

Project Console: https://console.firebase.google.com/project/PROJECT_ID/overview
```

2. Run `firebase dataconnect:compile`

```
$ firebase dataconnect:compile
✔  dataconnect: Successfully compiled SQL Connect service: test-dc-2
```

## Notes

not sure if experiments plays a role here, but here's the enabled experiments

```
 firebase experiments:list
┌─────────┬────────────────────────────────┬───────────────────────────────────────────────────────────────────────────────────────┐
│ Enabled │ Name                           │ Description                                                                           │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ functionsv2deployoptimizations │ Optimize deployments of v2 firebase functions                                         │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ dartfunctions                  │ Enable Dart Functions.                                                                │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ kits                           │ Enable Functions Kits.                                                                │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ webframeworks                  │ Native support for popular web frameworks                                             │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ pintags                        │ Adds the pinTag option to Run and Functions rewrites                                  │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ appcheckadmin                  │ Manage App Check enforcement and attestation providers from the CLI.                  │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ apphosting                     │ Allow CLI option for Frameworks                                                       │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ abiu                           │ Enable Automatic Base Image Updates (ABIU) and runtime selection for App Hosting      │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ genkit                         │ Enable Genkit related features.                                                       │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ appsinit                       │ Adds experimental `apps:init` command.                                                │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ mcp                            │ Adds experimental `firebase mcp` command for running a Firebase MCP server.           │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ fdcwebhooks                    │ Enable Firebase SQL Connect webhooks feature.                                         │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ fdcrealtime                    │ Enable Firebase SQL Connect realtime feature.                                         │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ secretEnvParams                │ Enable reading the backing resource binding for a Functions secret param from .env    │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ extdeprecationwarnings         │ Show deprecation warnings for Firebase Extensions CLI commands.                       │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ y       │ extMigrationFeatures           │ Enable features intended to assist with the migration of Extension instances to Kits. │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ n       │ deletegcfartifacts             │ Add the functions:deletegcfartifacts command to purge docker build images             │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ n       │ legacyRuntimeConfigCommands    │ Expose legacy functions.config() CLI commands                                         │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ n       │ mcpalpha                       │ Opt-in to early MCP features before they're widely released.                          │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ n       │ mcpapps                        │ Enables MCP Apps features                                                             │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ n       │ apptesting                     │ Adds experimental App Testing feature                                                 │
├─────────┼────────────────────────────────┼───────────────────────────────────────────────────────────────────────────────────────┤
│ n       │ crashlyticsWeb                 │ Enable the ability to upload source maps for web apps to Crashlytics.                 │
└─────────┴────────────────────────────────┴───────────────────────────────────────────────────────────────────────────────────────┘
```

<!-- TITLE: Developing For Persona Locally -->
<!-- SUBTITLE: A quick guide for devloping for Persona locally -->

# Developing For Persona Locally

Persona has two different environments, *Sandbox* and *Production*. For all testing and development, use the Sandbox environment. See Persona's [documentation](https://docs.withpersona.com/docs/environments) for up-to-date information.

## Frontend

The development environment defaults to using a Mock Persona Flow. This is selected by the buildpack based on the code below:

```typescript
// PersonaEmbeddedFlowLauncher.tsx

/// #if isEnvDevelopment
if (process.env.REACT_APP_ENVIRONMENT === 'development') {
  PersonaEmbeddedFlowLauncher = require('./MockPersonaEmbeddedFlowLauncher').default;
}
/// #endif
```

If you want to test the launchers with the actual flow locally, you will need to comment out that code so that the non-Mock luancher code gets loaded and compiled.

### ngrok

Persona uses Webhooks that make requests to our API with status updates for inquiries and verifications.

Because the launcher will be loaded for the Sandbox environment, any changes will trigger updates on the staging API and database--not your local dev environment. To correct this, you will need to use a service to expose your local port externally like [ngrok](https://ngrok.com).

To install ngrok, create a free account (you can auth with Google SSO) and follow [the instructions on ngrok's website](https://ngrok.com/download). Or on Linux:

```bash
sudo snap install ngrok
  ...
ngrok authtoken <your_auth_token>
```

Then once ngrok is installed and your authtoken is in place, you can point ngrok to your local API with:

```bash
ngrok http 3001
```

This generates a URL like `https://8be0af269dd3.ngrok.io` that you can copy from your terminal and use to point to your local API. There are existing webhooks in the Sandbox environment with ngrok.io URLs that are inactive by default. While you are developing go edit these and swap out the URL for your new URL, but leave the rest of the URL path after `ngrok.io`.

Now when you authenticate in the Sandbox environment, the changes should be reflected in your local enviornment!

_Make sure you deactivate the ngrok webhooks when you are done!_

_Make sure you end your ngrok session when you are done, too. Otherwise you may get some unwanted local traffic!_

## Backend

Using ngrok can be useful for the backend as well if you are testing changes in the frontend against the back end or vice versa.

To test our endpoints without the frontend, use the Mock Persona Service in the API code within the testing framework. There are many examples in the existing tests.

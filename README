# The Vite Federation Plugin
## A part of the MFE POC series

### Explanation
This repo is a working (mostly) demo of an MFE setup using the [vite-plugin-federation module](https://github.com/originjs/vite-plugin-federation). With it, we can build a series of applications with Vite and expose parts of said applications to be hosted by another (or others).

### Requirements
- A "host" application to import and compose all of the "remote" apps into a unified UI. This application is built with Vite and vite-plugin-federation. In the vite config file, it declares what apps/modules to import and URLs from which to import them. A host can also expose it's own modules.

Example:
```javascript
// vite.config.js
import federation from "@originjs/vite-plugin-federation";
export default {
    plugins: [
        federation({
            name: 'host-app',
            remotes: {
                remote_app: "http://localhost:5001/assets/remoteEntry.js",
            },
            shared: ['vue']
        })
    ]
}
```

- 1 to Many "remote" applications, configured to expose modules to be used by the host. Interestingly, the plugin is compatible with Webpack 5 Module Federation so remote apps can be built with either technology! In either case, the build config file for each app describes which modules to expose, then creates a "remoteEntry.js" file when built and serves that file to a URL which the host uses (can use other methods with further configuration).

Example:
```javascript
// vite.config.js
import federation from "@originjs/vite-plugin-federation";
export default {
    plugins: [
        federation({
            name: 'remote-app',
            filename: 'remoteEntry.js',
            // Modules to expose
            exposes: {
                './Button': './src/Button.vue',
            },
            shared: ['vue']
        })
    ]
}
```

### Considerations
Since the host app requires the remote apps to serve a build artifact, you cannot run remote apps in development mode inside the host shell. However, remote apps can run in dev mode stand-alone, without the host to facilitate easier development and built/served to the host for final "integration testing". It's worth noting, integration tasks could be slow and difficult.

Remote apps will have freedom to use whatever frameworks they choose, but it MUST be built with Vite + plugin, or webpack 5.

Since it's a 3rd party plugin, stability could be a concern. As of 06/03/24, it appears the library is still maintained but it cannot be guaranteed forever.

There are some code samples available for different framework configurations, but documentation as a whole is very lacking--especially so for more complex/unique configurations...
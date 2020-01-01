# About

Starter Amplify application using lambda, api gateway and cognito user auth.
[Reference here](https://github.com/ErikCH/Aws-auth-example)

# Create amplify application

```
amplify init
amplify push
```

# Build frontend
```
yarn
yarn build
```

# Deploy the frontend

First push the code to an amplify supported git repos such as github, gitlab etc. then
connect the frontend from the amplify application ui. Note that you might need to update
the serving path to 'dist'.

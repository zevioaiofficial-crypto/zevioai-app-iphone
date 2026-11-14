# Zevio AI iOS build package

This package prepares the Zevio AI frontend for a Codemagic iOS build.

## Build
1. Upload the contents of this ZIP to a GitHub repository (the `Zevio-AI` folder contents should be at repository root).
2. Connect that repository in Codemagic.
3. Select the `zevio-ai-ios-unsigned` workflow from `codemagic.yaml`.
4. Start a build and download `Zevio-AI-unsigned.ipa` from Artifacts if the build succeeds.

## Important: unsigned IPA
This workflow deliberately builds without Apple signing. An unsigned IPA cannot be installed directly. Sideloadly needs a correctly signed app. A free Apple Account may sign for personal testing with the normal free-account limitations; this does not create App Store distribution signing.

## Backend requirement
The IPA contains the React frontend only. It does not run the Node.js backend or the GPU inference server inside iOS. Deploy the backend and inference server separately, then configure the app to reach that backend. The current frontend API client supports a custom API base URL saved in its settings; a local `localhost:5000` backend will not be reachable from the iPhone.

## Security
Do not commit `.env` files, API keys, Supabase service-role keys, passwords, or private tokens.

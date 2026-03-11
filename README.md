# enjoin-jwks

Publicly available JWKS (JSON Web Key Set) repository that serves public keys for JWT verification across multiple environments.

## Overview

This repository hosts JSON Web Key Set (JWKS) endpoints used by the Enjoin platform for verifying JSON Web Tokens (JWTs). It provides a centralized, publicly accessible location for JWT public keys across different deployment environments.

## Repository Structure

```
enjoin-jwks/
├── docs/                    # GitHub Pages served content (public site root)
│   ├── index.html          # Landing page with JWKS endpoint links
│   ├── prod/               # Production environment JWKS
│   │   └── jwks.json
│   ├── non-prod/           # Non-production environment JWKS
│   │   └── jwks.json
│   └── sandbox/            # Sandbox/testing environment JWKS
│       └── jwks.json
└── README.md               # This file
```

## Deployment

This repository is configured to serve the `/docs` folder via **GitHub Pages**. Any changes committed to the `docs/` directory are automatically published to the live website.

## JWKS Endpoints

The following JWKS endpoints are publicly available for JWT verification:

- **Production**: `./docs/prod/jwks.json` → `https://<github-pages-url>/prod/jwks.json`
- **Non-Production**: `./docs/non-prod/jwks.json` → `https://<github-pages-url>/non-prod/jwks.json`
- **Sandbox**: `./docs/sandbox/jwks.json` → `https://<github-pages-url>/sandbox/jwks.json`

These can be accessed through the main landing page at the GitHub Pages URL.

## What is JWKS?

A JSON Web Key Set (JWKS) is a set of keys containing the public keys used to verify JSON Web Tokens (JWTs). Each key in the set includes:
- The public key material
- Key identifiers (kid)
- Key usage information
- Algorithm specifications

## Usage

Services that need to verify Enjoin JWTs should:

1. Fetch the appropriate JWKS endpoint for their environment
2. Extract the public key(s) matching the JWT's key ID (`kid` claim)
3. Use the public key to verify the JWT signature
4. Cache the JWKS data with appropriate TTL (typically 1 hour)

## Environments

- **Production** - Keys used in production deployments
- **Non-Production** - Keys for staging and development environments
- **Sandbox** - Keys for testing and sandbox environments

## GitHub Pages Configuration

The repository is configured with GitHub Pages to serve content from the `/docs` folder. This means:
- Any files in `/docs` are publicly accessible
- Changes to `/docs` are deployed automatically
- The site is live at the repository's GitHub Pages URL

## Security Notes

- Only public keys are stored in this repository
- These are safe to distribute publicly
- Never commit private keys to this repository
- Keys should be rotated periodically
- Verify JWT signatures before trusting token claims

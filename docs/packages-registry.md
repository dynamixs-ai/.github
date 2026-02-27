# GitHub Packages Registry

This document describes how to use the **dynamixs-ai** GitHub Packages Registry for publishing and consuming Docker images and Maven artifacts.

All packages are hosted at:

- **Container Registry:** `ghcr.io/dynamixs-ai`
- **Maven Registry:** `https://maven.pkg.github.com/dynamixs-ai`
- **Overview:** https://github.com/orgs/dynamixs-ai/packages

---

## Authentication

All packages in this organization are **private**. Authentication is required for both pushing and pulling artifacts.

### Step 1: Create a Personal Access Token (PAT)

Go to: **https://github.com/settings/tokens/new**

Create a **Classic Token** with the following scopes:

| Scope            | Required for                           |
| ---------------- | -------------------------------------- |
| `read:packages`  | Pulling images / downloading artifacts |
| `write:packages` | Pushing images / publishing artifacts  |

> **Important:** Copy the token immediately after creation – GitHub only shows it once!

> **Note:** If you already have an existing token, do not reuse it for GHCR. Create a dedicated new token – older tokens may not be properly initialized for the GitHub Container Registry even if the scopes are set correctly.

---

## Docker / Container Images

### Login

```bash
echo "YOUR_PAT" | docker login ghcr.io -u YOUR_GITHUB_USERNAME --password-stdin
```

On success you will see:

```
Login Succeeded
```

Docker stores the credentials in `~/.docker/config.json`, so you only need to login once.

### Build & Tag

```bash
VERSION=1.0.0

docker build -f ./docker/Dockerfile -t ghcr.io/dynamixs-ai/ai-platform:$VERSION .
docker tag ghcr.io/dynamixs-ai/ai-platform:$VERSION ghcr.io/dynamixs-ai/ai-platform:latest
```

### Push

```bash
docker push ghcr.io/dynamixs-ai/ai-platform:$VERSION
docker push ghcr.io/dynamixs-ai/ai-platform:latest
```

Or use the developer script:

```bash
./dev.sh -docker    # build image
./dev.sh -deploy    # push to GHCR
```

### Pull

```bash
docker pull ghcr.io/dynamixs-ai/ai-platform:latest
```

---

## Maven Artifacts

### Settings Configuration

Add the following to your `~/.m2/settings.xml`:

```xml
<settings>
  <servers>
    <server>
      <id>dynamixs-ai</id>
      <username>YOUR_GITHUB_USERNAME</username>
      <password>YOUR_PAT</password>
    </server>
  </servers>
</settings>
```

### Repository Configuration in pom.xml

```xml
<repositories>
  <repository>
    <id>dynamixs-ai</id>
    <url>https://maven.pkg.github.com/dynamixs-ai/YOUR_REPO</url>
  </repository>
</repositories>
```

---

## Understanding Token Scope

When you create a PAT on GitHub, you do **not** explicitly assign it to a specific organization. A PAT is always bound to your **personal GitHub account**.

The access restriction works indirectly: the token can only access resources that your personal account already has access to. So a token created by `rsoika` can access `dynamixs-ai` packages only because `rsoika` is a member of that organization – nobody else's token would grant access to your organization.

### Classic Tokens vs. Fine-grained Tokens

|                 | Classic Token                                 | Fine-grained Token                            |
| --------------- | --------------------------------------------- | --------------------------------------------- |
| Scope           | All orgs/repos your account can access        | Explicitly restricted to specific org/repo    |
| Granularity     | Coarse (e.g. `write:packages` for everything) | Fine (e.g. `read:packages` for one repo only) |
| Recommended for | Internal developers                           | Partners / external collaborators             |

For internal developers a Classic Token with `read:packages` / `write:packages` is acceptable. For partners, always use **Fine-grained Tokens** – they can be restricted explicitly to the `dynamixs-ai` organization and a specific repository, giving you full control. Partner tokens can be revoked at any time without affecting other users.

---

## Partner Access

Partners receive a dedicated **read-only token** with only the `read:packages` scope. This allows pulling images and downloading Maven artifacts, but does not allow publishing.

Contact the organization admin to request a partner token. The token can be revoked at any time without affecting other users.

### Docker Pull (Partners)

```bash
echo "PARTNER_TOKEN" | docker login ghcr.io -u YOUR_GITHUB_USERNAME --password-stdin
docker pull ghcr.io/dynamixs-ai/ai-platform:latest
```

---

## Troubleshooting

| Problem                          | Solution                                                                    |
| -------------------------------- | --------------------------------------------------------------------------- |
| `denied: denied` on docker login | Create a new token – do not reuse existing ones for GHCR                    |
| `UNAUTHORIZED` from curl test    | Token scopes incorrect or token not properly initialized                    |
| Maven deploy fails               | Check `~/.m2/settings.xml` server id matches the repository id in `pom.xml` |
| Package not visible on GitHub    | Private packages require authentication – anonymous access is not possible  |

# Security Policy

## What "security" means for this repository

This repository contains documents: a written case study, a reusable working-method, diagrams, work orders, and templates. It ships no executable code, no dependencies, and no runtime, so the realistic security surface is narrow. A few things are still worth reporting privately rather than in a public issue:

- A secret, private path, or personal datum accidentally committed to the repository or left in its git history.
- A malicious or misleading link inside the documents or diagrams.
- Content that could be read as operational instructions for defeating a safeguard. This project is analytical and defensive; anything that reads otherwise is a bug worth flagging.

## Reporting

Please report privately, not as a public issue:

1. Use GitHub's **Security** tab on this repository, then "Report a vulnerability", or
2. contact the maintainer directly at the email listed on the maintainer's GitHub profile (`acsole`).

Please include what you found, where, and why it concerns you. Reports will be acknowledged as promptly as possible.

## Secrets and credentials

This project never stores API keys, tokens, or credentials: it has no code that would need them. If you spot anything secret-looking in the files or history, report it as above. If something sensitive was committed by mistake, it will be revoked or rotated at the source and then removed by rewriting history, since it otherwise remains reachable in past commits.

## Scope and limitations (disclosed transparently)

- This is a case study and a working-method, not a production system or a security product. As the README states under "What this is NOT", there is no measured detection rate, and none is claimed.
- The safeguards discussed are analyzed for where they break at scale. The intent is defensive understanding, not an operational playbook.

## Supported versions

This is a single-track project. Corrections are applied to the `main` branch only.

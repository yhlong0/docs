---
title: "Override public key"
sidebar_position: 9
description: "Configure public key authentication for secure access via terminal, or override at the pod level using the RUNPOD_SSH_PUBLIC_KEY environment variable."
---

We attempt to inject the public key that you configure in your account's settings page for authentication using basic terminal.
If you want to override this at a pod level, you can manually supply a public key as the `RUNPOD_SSH_PUBLIC_KEY` environment variable.

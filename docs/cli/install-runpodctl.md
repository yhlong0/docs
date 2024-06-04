---
title: Installing runpodctl
description: "Get started with runpodctl, an open-source CLI, to work with Pods and RunPod projects. Install and configure the tool, then verify the installation and API key setup to start using runpodctl."
sidebar_position: 1
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import CodeBlock from '@theme/CodeBlock';

runpodctl is an [open-source command-line interface (CLI)](https://github.com/runpod/runpodctl). You can use runpodctl to work with Pods and RunPod projects.

When you create a Pod, it comes with runpodctl installed and configured with a Pod-scoped API key. You can also run runpodctl locally.

To install runpodctl on your local machine, run the appropriate command for your operating system.

<Tabs>
  <TabItem value="mac" label="macOS">

<CodeBlock language="bash">
brew install runpod/runpodctl/runpodctl
</CodeBlock>

</TabItem>
  <TabItem value="linux" label="Linux">

<CodeBlock language="bash">
wget -qO- cli.runpod.net | sudo bash
</CodeBlock>

</TabItem>
  <TabItem value="windows" label="Windows">

<CodeBlock language="bash">
wget https://github.com/runpod/runpodctl/releases/download/v1.12.3/runpodctl-windows-amd64.exe -O runpodctl.exe
</CodeBlock>

</TabItem>
</Tabs>

## Configuring runpodctl

Before you can use runpodctl, you must configure an API key. To create a new API key, complete the following steps:

1. In the web interface, go to your [**Settings**](https://www.runpod.io/console/user/settings).
2. Expand **API Keys** and click the **+ API Key** button.
3. Select **Read** or **Read & Write** permissions.
4. Click **Create**.

:::note

Keep your API key secret. Anyone with the key can gain full access to your account.

:::

Now that you've created an API key, run the following command to add it to runpodctl:

<CodeBlock language="bash">
runpodctl config --apiKey your-api-key
</CodeBlock>

You should see something similar to the following output:

<CodeBlock language="bash">
saved apiKey into config file: /Users/runpod/.runpod/config.toml
</CodeBlock>

Now that you've configured an API key, check that runpodctl installed successfully. Run the following command:

<CodeBlock language="bash">
runpodctl version
</CodeBlock>

You should see which version is installed.

<CodeBlock language="bash">
runpodctl v1.13.0
</CodeBlock>

If at any point you need help with a command, you can use the `--help` flag to see documentation on the command you're running.

<CodeBlock language="bash">
runpodctl --help
</CodeBlock>

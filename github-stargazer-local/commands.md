### Download fluvio version manager and fluvio components

```bash
curl -fsS https://hub.infinyon.cloud/install/install.sh | bash
```

Copy and run the last line of the install log to update PATH.

### Start local fluvio cluster

```bash
fluvio cluster start
```

### Ensure you are in the correct directory:

```bash
cd [path to github-stargazer-local]
```

### Update the secrets file with the relevant tokens for Slack and Discord

```bash
nano secrets.txt
```

add the values relevant to you
```bash
DISCORD_TOKEN=
SLACK_TOKEN=
GITHUB_TOKEN=
```

### Start the connectors

**Inbound - Github**

```bash
cdk deploy start --ipkg infinyon-http-source-0.3.1.ipkg --config github.yaml --secrets secrets.txt
```

**Outbound - Discord**

```bash
cdk deploy start --ipkg infinyon-http-sink-0.2.6.ipkg --config discord.yaml --secrets secrets.txt
```

**Outbound - Slack**

```bash
cdk deploy start --ipkg infinyon-http-sink-0.2.6.ipkg --config slack.yaml --secrets secrets.txt
```

### List connectors and delete connectors if you need to troubleshoot

```bash
cdk deploy list
```

```bash
cdk deploy shutdown --name github-stars-inbound
```

```bash
cdk deploy shutdown --name discord-stars-outbound
```

```bash
cdk deploy shutdown --name slack-stars-outbound
```

### Delete fluvio cluster if you wish to start over or need to clean up:

This will delete topics and smart modules as well as connectors. Only the config files and the connector packages will remain.

```bash
fluvio cluster delete
```

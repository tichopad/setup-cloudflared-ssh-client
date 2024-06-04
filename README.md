# setup-cloudflared-ssh-client

SSH servers exposed via Cloudflare Tunnel require a special setup to connect to them. See [Cloudflare Tunnel documentation](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/use-cases/ssh/#2-connect-as-a-user) for more information.

This GitHub Action sets up everything required to connect to an SSH server exposed via Cloudflare Tunnel from inside of a runner.

> [!WARNING]
>
> This action only supports Ubuntu runners.

## Usage

```yaml
jobs:

  do-the-thing:

    runs-on: ubuntu-latest

    steps:

      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Setup SSH client for Cloudflare Tunnel
        uses: tichopad/setup-cloudflared-ssh-client@v1
        with:
          hostname: example.com

      - name: Connect to SSH server
        run:  ssh -T user@example.com 'echo "Hello, world!"'
```

You can combine this action with [tichopad/setup-ssh-client](https://github.com/tichopad/setup-ssh-client) for a general SSH client setup with Cloudflare Tunnels:

```yaml
jobs:

  do-the-thing:

    runs-on: ubuntu-latest

    steps:

      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Setup SSH client
        uses: tichopad/setup-ssh-client@v1
        with:
          ssh-key: ${{ secrets.SSH_KEY }}

      - name: Setup SSH client for Cloudflare Tunnel
        uses: tichopad/setup-cloudflared-ssh-client@v1
        with:
          hostname: example.com

      - name: Connect to SSH server
        run:  ssh -T user@example.com 'echo "Hello, world!"'
```
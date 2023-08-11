# SSH to GitHub Actions

This GitHub Action offers you connect to GitHub Actions VM via SSH for interactive debugging

## Features

- Support Ubuntu and macOS
- Provides two optional SSH connection methods, tmate and ngrok
- Proceed to the next step to stay connected
- Send SSH connection info to Telegram

## Usage

```yaml
- name: SSH2action
  uses: 1-1-2/SSH2Actions@main
  with:
    # choose backend [tmate, ngrok] (optional, default 'tmate').
    mode: tmate
  env:
    # Enable background mode [false, true] (optional, default 'false').
    # In foreground mode, action will print connection infomation to log
    # and hold the step till `touch /tmp/continue`.
    # In background mode, action will write connection infomation to /tmp/conn.inf
    # then end the step.
    IN_BACKGROUND: false

    # After sign up on the https://ngrok.com
    # You can find this token here: https://dashboard.ngrok.com/auth/your-authtoken
    NGROK_TOKEN: ${{ secrets.NGROK_TOKEN }}
    
    # ngrok server region [us, eu, au, ap, sa, jp, in] (optional, default: us)
    # You can find this server region here: https://ngrok.com/docs#global-locations
    NGROK_REGION: us

    # This password you will use when authorizing via SSH
    SSH_PASSWORD: ${{ secrets.SSH_PASSWORD }}

    # Send connection info to Telegram (optional)
    # You can find related documents here: https://core.telegram.org/bots
    TELEGRAM_BOT_TOKEN: ${{ secrets.TELEGRAM_BOT_TOKEN }}
    TELEGRAM_CHAT_ID: ${{ secrets.TELEGRAM_CHAT_ID }}
```

## Example

### Connect to Github Actions VM via SSH by using [tmate](https://tmate.io)

```yaml
- name: Start SSH via tmate
  uses: 1-1-2/SSH2Actions@main
```

### Connect to Github Actions VM via SSH by using [ngrok](https://ngrok.com)

```yaml
- name: Start SSH via ngrok
  uses: 1-1-2/SSH2Actions@main
  with:
    mode: ngrok
    bg_mode: false
  env:
    NGROK_TOKEN: ${{ secrets.NGROK_TOKEN }}
    NGROK_REGION: us
    SSH_PASSWORD: ${{ secrets.SSH_PASSWORD }}
```

## Lisence

[MIT](https://github.com/1-1-2/SSH2Actions/blob/main/LICENSE) © 1-1-2

## Original

Thanks [P3TERX/ssh2actions](https://github.com/P3TERX/ssh2actions)


# dodo-migrate
A CLI-first migration toolkit to help teams move content from other payment providers or MoR platforms (e.g., LemonSqueezy, Gumroad, 2Checkout, FastSpring, Stripe, Paddle) into Dodo Payments. Focused on safety, auditability, and repeatable runs.

Supported providers: [Lemon Squeezy](./docs/lemonsqueezy/README.md)

### Usage:
Pre-Usage Requirements: Provider's API Key, Dodo Payments API key.  

Installation:
```
npm i -g dodo-migrate
```

Usage:
```
dodo-migrate [provider] [arguments (optional)]
```

Example (to move contents from Lemon Squeezy to Dodo Payments):
```
dodo-migrate lemonsqueezy
```
It will then prompt you to enter your API keys and then other required information.

<br/>

Update:
```
npm update -g dodo-migrate
```

Uninstall
```
npm uninstall -g dodo-migrate
```


### Detailed documentation:
You can find the individual documentation for each of the currently available providers below:  
- [Lemon Squeezy](./docs/lemonsqueezy/README.md)

### Roadmap:
- Add more providers
- Add more data options to move from current providers

### Contributing
Are you interested in contributing this repository?  
Check out the [contributing.md](./contributing.md) to learn more about the various guidelines to contribute!
# Stripe Node.js Library

[![Version](https://img.shields.io/npm/v/stripe.svg)](https://www.npmjs.org/package/stripe)
[![Build Status](https://github.com/nodoubtz/stripe-node/actions/workflows/main.yml/badge.svg?branch=main)](https://github.com/nodoubtz/stripe-node/actions?query=branch%3Amain)
[![Downloads](https://img.shields.io/npm/dm/stripe.svg)](https://www.npmjs.com/package/stripe)

The Stripe Node.js library provides seamless access to the Stripe API for server-side JavaScript applications. It includes examples for integration, secure management of API keys, and usage in various frameworks like Express, Koa, and Next.js.

## Table of Contents
- [Documentation](#documentation)
- [Requirements](#requirements)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Examples](#examples)
- [Security Practices](#security-practices)
- [Contributing](#contributing)
- [Support](#support)

## Documentation
- Full API reference: [Stripe Node.js API Docs](https://stripe.com/docs/api?lang=node)
- For browser-side integration, see [Stripe.js](https://stripe.com/docs/js).

## Requirements
- Node.js 12 or higher
- Stripe account ([sign up here](https://dashboard.stripe.com/register)).

## Installation
Install the library using your preferred package manager:
```bash
npm install stripe
# or
yarn add stripe
```

## Quick Start
Set up the library with your Stripe API secret key:
```javascript
const stripe = require('stripe')('sk_test_...'); // Replace with your secret key

stripe.customers.create({
    email: 'customer@example.com',
}).then(customer => console.log(customer.id))
.catch(error => console.error(error));
```

### Using ES Modules and Async/Await
```javascript
import Stripe from 'stripe';
const stripe = new Stripe('sk_test_...');

const customer = await stripe.customers.create({
    email: 'customer@example.com',
});

console.log(customer.id);
```

## Examples
### Creating a Product and Price
```javascript
const stripe = require('stripe')('sk_test_...');

const product = await stripe.products.create({
    name: 'Starter Subscription',
    description: '$12/Month subscription',
});

const price = await stripe.prices.create({
    product: product.id,
    unit_amount: 1200,
    currency: 'usd',
    recurring: { interval: 'month' },
});

console.log(`Product ID: ${product.id}`);
console.log(`Price ID: ${price.id}`);
```

For more examples, visit the [examples folder](./examples).

## Security Practices
- **Secure API Keys**: Never hardcode your API keys into the codebase. Use environment variables or a secure secrets management service.
- **Webhook Verification**: Always verify webhook signatures to ensure events are sent by Stripe.
  ```javascript
  const event = stripe.webhooks.constructEvent(
      rawBody, // Raw request body
      signatureHeader, // Stripe's signature header
      endpointSecret // Your webhook secret
  );
  ```
- Review and follow Stripe's [security best practices](https://stripe.com/docs/security).

## Contributing
We welcome contributions! Please follow these steps:
1. Fork the repository and create your branch from `main`.
2. Follow the [contribution guidelines](CONTRIBUTING.md).
3. Run tests before submitting:
   ```bash
   npm test
   ```

## Support
If you encounter issues or have questions, please consult the following resources:
- [Stripe Support](https://support.stripe.com/)
- [GitHub Issues](https://github.com/nodoubtz/stripe-node/issues)

---

Happy Coding! 🎉

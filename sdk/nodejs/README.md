# @ozanyurtsever/pulumi-stripe

A Pulumi provider for creating and managing Stripe resources, based on the [terraform-provider-stripe](https://github.com/lukasaron/terraform-provider-stripe) v3.3.3.

## Features

This package provides Pulumi bindings for Stripe resources including:

### Core Resources
- **Products** - Manage Stripe products
- **Prices** - Configure pricing for products  
- **Customers** - Manage customer records
- **Coupons** - Create discount coupons
- **Tax Rates** - Set up tax configurations
- **Webhook Endpoints** - Configure webhook listeners
- **Portal Configuration** - Customer portal settings
- **Shipping Rates** - Shipping cost configurations
- **Files** - File upload management

### New in v3.3.3
- **🆕 Meter** - Usage metering for billing (v3.3.0)
- **🆕 Entitlements Feature** - Feature entitlements (v3.2.0)  
- **🆕 Product Feature** - Product-specific features (v3.1.0)

## Installation

```bash
npm install @ozanyurtsever/pulumi-stripe
```

## Usage

```typescript
import * as stripe from "@ozanyurtsever/pulumi-stripe";

// Create a product
const product = new stripe.Product("my-product", {
    name: "My SaaS Product",
    description: "A great SaaS offering",
});

// Create a price for the product
const price = new stripe.Price("my-price", {
    currency: "usd",
    product: product.id,
    unitAmount: 999, // $9.99
    recurring: {
        interval: "month",
    },
});

// Create a meter for usage tracking (new in v3.3.0)
const meter = new stripe.Meter("api-requests", {
    displayName: "API Requests",
    eventName: "api_request",
});
```

## Configuration

Before using this provider, you need to configure your Stripe API key:

```bash
pulumi config set stripe:apiKey sk_test_... --secret
```

## Version History

- **v3.3.3** - Updated to terraform-provider-stripe v3.3.3
  - Added Meter resource for usage metering
  - Added Entitlements Feature support
  - Added Product Feature management
  - Breaking changes from v2.0.0: `tax_behaviour` → `tax_behavior`
  - Breaking changes from v3.0.0: Removed SubscriptionPause, Features → MarketingFeatures

## License

Apache-2.0

## Links

- [Terraform Provider Source](https://github.com/lukasaron/terraform-provider-stripe)
- [Original Pulumi Bridge](https://github.com/georgegebbett/pulumi-stripe)
- [Stripe API Documentation](https://stripe.com/docs/api)
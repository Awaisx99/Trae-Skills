# Skill: WooCommerce E-Commerce

## Purpose
To build, customize, and maintain WooCommerce online stores, including product management, checkout customization, payment gateways, and store optimization.

## When to Use
- Building new online stores
- Customizing existing WooCommerce sites
- Adding custom product features
- Modifying checkout flow
- Integrating payment gateways
- Optimizing store performance

## Procedure

### 1. Product Management
- Create Simple, Variable, Grouped, and External products
- Use product categories and tags for organization
- Set product prices, inventory, shipping, and attributes
- Use product galleries and featured images

### 2. Theme Customization
Override WooCommerce templates in your theme:
```
your-theme/woocommerce/
├── single-product/
│   └── title.php
├── cart/
│   └── cart.php
└── checkout/
    └── form-checkout.php
```
- Use WooCommerce hooks to modify pages:
  ```php
  add_action('woocommerce_before_single_product', 'my_custom_message');
  function my_custom_message() {
      echo '<p>Welcome to our store!</p>';
  }
  ```

### 3. Checkout Customization
- Use `woocommerce_checkout_fields` filter to modify checkout fields:
  ```php
  add_filter('woocommerce_checkout_fields', 'custom_checkout_fields');
  function custom_checkout_fields($fields) {
      // Modify or add fields here
      return $fields;
  }
  ```
- Customize the thank you page
- Add custom order statuses

### 4. Payment & Shipping
- Use built-in payment gateways (Stripe, PayPal, etc.)
- Add custom payment gateways
- Configure shipping zones and methods
- Use shipping classes for different product types

### 5. Performance & Security
- Keep WooCommerce updated
- Use SSL/HTTPS for checkout
- Use WooCommerce-specific security plugins
- Optimize product images
- Use caching compatible with WooCommerce

## Constraints
- Always test payment gateways in sandbox mode first
- Back up your store before making major changes
- Follow WooCommerce Developer Guidelines (https://woocommerce.com/document/developing-woocommerce-extensions/)
- Test checkout flow on multiple devices/browsers

## Expected Output
A secure, functional, and user-friendly WooCommerce online store.

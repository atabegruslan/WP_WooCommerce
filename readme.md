# Most Basic Setup

https://www.youtube.com/watch?v=lL15EarPKbE

1. Have these: 
- https://wordpress.org/plugins/woocommerce/
- https://wordpress.org/plugins/woocommerce-gateway-stripe/

2. Sign up at https://dashboard.stripe.com/

3. Copy over the credentials

https://docs.woocommerce.com/document/stripe/

![]()

4. Create new product and purchase

# Stripe API: https://stripe.com/docs

Create product and prices: 

- https://stripe.com/docs/api/products/create
- https://stripe.com/docs/invoicing/prices-guide

https://git.elidev.info/nhanlt/promonco/blob/dev/wp-content/themes/promonco/app/Components/Hooks/Admin/AdminActions.php#L278

When sync to stripe, use this hook: https://developer.wordpress.org/reference/hooks/pre_post_update/

Create subscription payment:

https://stripe.com/docs/billing/invoices/subscription#first-invoice-extra
    
https://git.elidev.info/nhanlt/promonco/blob/dev/wp-content/plugins/elinext-stripe-subscription/elinext-stripe-subscription.php#L355

`$response = WC_Stripe_API::request($attachData, $url, 'POST');`

Utilize: `/wp-content/plugins/woocommerce-gateway-stripe/includes/class-wc-stripe-api.php`

```php
$attachData = [
                'default_tax_rates' => [
                    "$tax->id" 
                ],
                'customer'          => $customerId,
                'items'             => [[ 'price' => $stripeSubscriptionPriceId ]], // For subscription
                'add_invoice_items' => [[ 'price' => $stripeOneTimePriceId ]] // For one-time payment
            ];

            $url = WC_Stripe_Subscription::_URL_SUBSCRIPTION;//'subscriptions'
            
            $response = WC_Stripe_API::request($attachData, $url, 'POST');
```

# WooCommerce

https://wordpress.stackexchange.com/questions/307/where-can-i-find-a-list-of-wordpress-hooks

https://woocommerce.github.io/code-reference/hooks/hooks.html

http://hookr.io/plugins/woocommerce/3.0.6/#index=a

https://www.businessbloomer.com/woocommerce-visual-hook-guide-checkout-page/

https://docs.woocommerce.com/document/hook-filter-reference/

## Language

https://docs.woocommerce.com/document/woocommerce-localization/

# Paypal

https://wordpress.org/plugins/wp-paypal/

https://www.wpbeginner.com/plugins/10-wordpress-paypal-plugins-for-easily-accepting-payments/

https://www.wpbeaverbuilder.com/best-wordpress-paypal-plugins/

# Stripe

https://www.youtube.com/watch?v=26hVzxp6hmc

https://www.youtube.com/watch?v=KlcqEVAO8y4

https://www.youtube.com/watch?v=Z-tGVDfzL9g

https://www.youtube.com/watch?v=lQUI2R7XbiU

https://www.youtube.com/watch?v=mI_-1tbIXQI

## Stripe Subscription plugins

https://templatic.com/wp/wordpress-subscription-plugins-woocommerce-subscription-alternatives/

https://www.webtoffee.com/woocommerce-subscription-stripe-payment-gateway/

https://woocommerce.com/products/woocommerce-subscriptions/

## Override Email

Override

`wp-content/plugins/woocommerce/templates/emails/customer-invoice.php`

with 

`wp-content/themes/{yourtheme}/woocommerce/emails/customer-invoice.php`

If you are overriding a plugin's template, and that plugin is built upon WooCommerce (eg `woocommerce-subscriptions`), then your override would be `.../{yourtheme}/woocommerce/...` not `.../{yourtheme}/woocommerce-subscriptions/...`.

# Notes

Get custom field

https://wordpress.stackexchange.com/questions/260442/how-to-get-all-custom-fields-of-any-post-type

https://metabox.io/get-post-custom-field-wordpress-p2/

Intercept Saves

admin_post_action: https://blog.wplauncher.com/add-wordpress-admin-post-action/

WP pre_post_update: https://developer.wordpress.org/reference/hooks/pre_post_update/

acf/pre_save_post: https://www.advancedcustomfields.com/resources/acf-pre_save_post/

WP save_post: https://developer.wordpress.org/reference/hooks/save_post/

acf/save_post: https://stackoverflow.com/questions/34853075/wordpress-acf-when-save-post

WP save_post_type: https://developer.wordpress.org/reference/hooks/save_post_post-post_type/

WooEC save_post_product: https://www.mootpoint.org/blog/woocommerce-hook-product-updated-added/

ACF

https://www.advancedcustomfields.com/resources/get_field/

https://www.advancedcustomfields.com/resources/get_sub_field/

https://www.advancedcustomfields.com/resources/update_field/

Metabox

https://diveinwp.com/add-custom-metabox-and-save-get-meta-box-value-in-wordpress/

https://stackoverflow.com/questions/66021598/woocommerce-add-admin-custom-fields-to-simple-subscriptions

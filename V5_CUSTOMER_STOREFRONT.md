# V5 customer storefront notes

## Pages and interactions
The `/` route is the customer storefront. It contains:
- Brand header, catalogue search, account action and cart count.
- Hero section and service-value statements.
- Category filters and product cards.
- Cart drawer with quantity adjustment and item removal.
- Sign-up/sign-in modal using Supabase Auth email/password.
- Checkout form for Gulu City delivery details and payment method.
- Seller-interest call to action.

## Live data behavior
The page requests `/api/products`. When active products are returned, it uses those records. If the catalogue is empty or the API is unavailable, it shows sample preview items with ordering disabled. This prevents sample items from being mistaken for real stock.

## Checkout behavior
A customer must be signed in. Checkout sends product IDs and quantities to `POST /api/orders` with the Supabase access token. The server remains responsible for product prices, stock validation, commission calculations and order creation. The browser does not submit a trusted total.

The Mobile Money options are marked as not activated. The order API currently creates a pending order but does not initiate or verify a payment-provider transaction. Do not represent these options as live until a payment integration and webhook verification have been completed.

## Before public launch
1. Set the production Supabase URL and anon key.
2. Review database migrations, row-level security and all service-role API access.
3. Add secure account recovery, email/phone verification and abuse protections.
4. Configure image storage and validate uploaded image types/sizes.
5. Implement a delivery fee rule for Gulu City and rider/dispatch workflow.
6. Connect an approved Mobile Money aggregator; verify callbacks/signatures and idempotency.
7. Add order confirmation and status notifications.
8. Complete seller application approval, seller product management, subscription billing, commission ledger and manual payout approval/recording screens.
9. Run automated tests, accessibility checks, mobile device tests and a production build.
10. Deploy to a hosting provider, configure domain/HTTPS, backups, monitoring and support contact.

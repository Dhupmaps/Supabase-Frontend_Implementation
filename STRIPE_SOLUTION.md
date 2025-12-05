# Stripe Integration Strategy

To implement an application fee using Stripe Checkout:

1. Create Session: The backend calls `stripe.checkout.sessions.create`.
2. Application Fee: Inside this call, we pass the `payment_intent_data` object containing `application_fee_amount: 500` (e.g., $5.00) to split the payment between the platform and the counselor.
3. Redirect: The server returns a Session ID; the frontend redirects the user to the Stripe hosted page.
4. Webhook: We set up a webhook endpoint listening for `checkout.session.completed`.
5. Fulfillment: When the webhook fires, we verify the signature, retrieve the metadata (application ID), and update the database status to "paid".
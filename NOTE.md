## What I picked

Return policy contradiction.
Cart footer says: "Free returns in 30 days."
Product schema says: `returnFees: FreeReturn`.
Actual return policy says customers pay return shipping unless the item is faulty.
All three are live right now, disagreeing with each other.

## Why it's the highest-impact thing here

I spent time checking the obvious stuff first — Bundle Builder, cart drawer, performance, template suffix issues.
Those are real, but they are loud bugs. I wanted to find the quieter one other people might miss.

This one can cost money today. Not tomorrow. Not in two weeks.
Google reads `hasMerchantReturnPolicy.returnFees` from Product structured data. If the value says `FreeReturn`, Google is eligible to show inaccurate return information next to Xinzuo products in search.

For an Australian store, that is not just bad data. Return-cost wording before purchase needs to be accurate. If the policy says the customer pays return shipping, the theme should not tell Google or customers that returns are free.may cause compliance issues

A visible broken page is annoying. This is worse: it is the store making a promise the policy does not support.

Trust is money in ecommerce.

## What I did

Changed `FreeReturn` to `ReturnFeesCustomerResponsibility` in both schema locations:
- `sections/product-information.liquid`
- `sections/featured-product.liquid`

I considered `ReturnShippingFees`, but that implies a fixed merchant-defined return fee with an amount. The policy does not set a fixed fee. It puts return shipping responsibility on the customer.
So `ReturnFeesCustomerResponsibility` is the right enum.

I also changed the cart copy from:
"Free returns in 30 days"
to:
"30-day returns"

The 30-day window is accurate. The word "Free" is not.

Three files. One issue.

## What I'd do next

Saw Bundle Builder template_suffix , preload issue & cart issue, will probably fix them

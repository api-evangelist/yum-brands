# Yum! Brands GraphQL Schema

## Overview

This is a conceptual GraphQL schema for the Yum! Brands Byte by Yum! platform, covering the digital ordering, loyalty, menu management, restaurant operations, and delivery capabilities across KFC, Pizza Hut, Taco Bell, and The Habit Burger Grill brands.

Yum! Brands operates over 63,000 restaurants in 155 countries. The Byte by Yum! platform is an AI-driven technology layer that powers customer-facing digital ordering and team-member-facing operational tools across all four brands.

## Schema Source

Conceptual schema derived from public documentation, press releases, and known capabilities of the Byte by Yum! platform at [https://www.yum.com/wps/portal/yumbrands/Yumbrands/bytebyyum](https://www.yum.com/wps/portal/yumbrands/Yumbrands/bytebyyum).

## Schema File

- [yum-brands-schema.graphql](yum-brands-schema.graphql)

## Key Types

### Brand and Restaurant

- `Brand` — top-level brand entity (KFC, Pizza Hut, Taco Bell, Habit Burger)
- `Restaurant` — individual restaurant location with store number, address, hours, and capabilities
- `RestaurantDetails` — extended attributes including drive-through, dine-in, delivery, and catering availability
- `StoreHours` — operating hours by day of week and meal period
- `Location` — geographic coordinates and address components
- `StoreNumber` — brand-specific store identifier and franchisee association

### Menu

- `Menu` — full menu for a brand or specific restaurant
- `MenuCategory` — grouping of items (e.g., Burgers, Sides, Drinks)
- `MenuItem` — individual menu item with name, description, pricing, and images
- `MenuItemDetails` — extended item information including nutrition, allergens, and modifications
- `Combo` — bundled meal combination
- `ComboItem` — individual component within a combo
- `SizeOption` — size variants and associated pricing
- `Modification` — available customizations for a menu item
- `Addons` — additional items that can be added to an order

### Nutrition and Allergens

- `Nutrition` — calorie, fat, protein, carbohydrate, and sodium data per serving
- `Allergens` — allergen flags including gluten, dairy, nuts, eggs, soy, shellfish

### Ordering

- `Order` — customer order with items, totals, payment, and status
- `CartItem` — line item in an active cart
- `CartModification` — applied modification to a cart item
- `OrderSummary` — high-level order confirmation data
- `OrderTotal` — subtotal, taxes, fees, and grand total breakdown
- `Tax` — tax line with jurisdiction and rate
- `Fee` — service, delivery, or convenience fees

### Payment

- `PaymentMethod` — abstract payment type
- `Cash` — cash payment details
- `Card` — credit or debit card details
- `Digital` — digital wallet (Apple Pay, Google Pay)
- `Payment` — applied payment record with amount and status

### Promotions and Loyalty

- `Promotion` — time-bound discount or offer
- `Deal` — bundled pricing promotion
- `SpecialOffer` — limited-time or targeted offer
- `CouponCode` — redeemable coupon with discount value
- `LoyaltyPoints` — points balance and transaction history
- `RewardProgram` — brand loyalty program details and tiers

### Brand-Specific Types

- `KFC` — KFC-specific attributes (Colonel's Club loyalty, bucket meals)
- `PizzaHut` — Pizza Hut-specific attributes (Hut Rewards, pizza builder)
- `TacoBell` — Taco Bell-specific attributes (Live Mas loyalty, customization matrix)
- `HabitBurger` — The Habit Burger Grill specific attributes (Habit Rewards, char-grilled menu)

### Delivery

- `Delivery` — delivery order with address, driver, and estimate
- `Driver` — delivery driver information
- `DeliveryEstimate` — estimated preparation and delivery time windows
- `OrderTracking` — real-time order status and driver location
- `OrderStatus` — enumeration of order lifecycle states

### Customer and Account

- `Customer` — registered customer profile
- `CustomerAccount` — account details including payment methods and saved addresses
- `AccountHistory` — past orders and loyalty activity

### Developer and Integration

- `APIKey` — developer API key with scopes and rate limits
- `Token` — authentication token with expiry
- `Webhook` — registered webhook endpoint with event subscriptions
- `Feedback` — customer-submitted feedback record
- `Rating` — numeric rating with context
- `Review` — detailed written review with rating

## Queries

- `brand(id: ID!)` — fetch a single brand by ID
- `brands` — list all Yum! Brands brands
- `restaurant(id: ID!)` — fetch a single restaurant location
- `restaurants(brandId: ID, location: LocationInput, radius: Float)` — search restaurants by brand and proximity
- `menu(restaurantId: ID!, serviceMode: ServiceMode)` — fetch the menu for a specific restaurant
- `menuItem(id: ID!)` — fetch a single menu item
- `order(id: ID!)` — fetch an order by ID
- `orderTracking(orderId: ID!)` — fetch real-time tracking for a delivery order
- `customer(id: ID!)` — fetch customer profile
- `loyaltyPoints(customerId: ID!, brandId: ID!)` — fetch loyalty balance
- `promotions(brandId: ID!, restaurantId: ID)` — list active promotions

## Mutations

- `createOrder(input: OrderInput!)` — submit a new order
- `updateCart(input: CartInput!)` — add or modify items in a cart
- `applyPromotion(orderId: ID!, code: String!)` — apply a coupon or promotion
- `redeemLoyaltyPoints(customerId: ID!, brandId: ID!, points: Int!)` — redeem loyalty points
- `submitFeedback(input: FeedbackInput!)` — submit customer feedback
- `registerWebhook(input: WebhookInput!)` — register a webhook endpoint

## Subscriptions

- `orderStatusUpdated(orderId: ID!)` — real-time order status updates
- `driverLocationUpdated(orderId: ID!)` — real-time driver location during delivery

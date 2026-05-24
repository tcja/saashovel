# SaaShovel Documentation

Welcome to the SaaShovel Documentation! This guide provides everything you need to know to set up, customize, and get the most out of SaaShovel. Whether you're just getting started or looking to explore advanced features, this documentation will help you make the most of your SaaS experience with SaaShovel.
Check out our GitHub repository for the latest code and updates.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Get Started](#get-started)
- [Commands](#commands)
- [Billing Providers](#billing-providers)
- [Layouts](#layouts)
- [Localization](#localization)
- [Admin Panel](#admin-panel)
- [Dashboard Customization](#dashboard-customization)
- [App Customization](#app-customization)
- [Components](#components)
- [Page Customization](#page-customization)
- [Permissions](#permissions)
- [Database & Seeding](#database-seeding)
- [Themes](#themes)
- [Security](#security)
## Prerequisites

### System Requirements

### Core Requirements

PHP ≥ 8.2
Node.js (for asset compilation)
Composer (PHP package manager)
MySQL 5.7+ or PostgreSQL 9.6+
### PHP Extensions

IMAGICK PHP Extension (in order to access the latest versions of the auth screens package)
GMP PHP Extension (if not installed, the Google Analytics widgets in the admin panel will fail to display)
BCMath PHP Extension
Ctype PHP Extension
JSON PHP Extension
MBSTRING PHP Extension
MYSQLI PHP Extension
OpenSSL PHP Extension
PDO PHP Extension
Tokenizer PHP Extension
XML PHP Extension
FILEINFO PHP Extension
### Key Dependencies

Laravel v11.x
Livewire v3.x
Filament v3.2+
TailwindCSS v3.4+
### Development Environment

We recommend using one of these options for the best development experience:
- Laravel Herd (Windows/macOS) - fastest native environment
- Laravel Sail (all platforms) - Docker-based solution
- Laragon (Windows) - full-featured local server
- Laravel Valet (macOS) - lightweight option
- Laravel Homestead (all platforms) - VM-based environment

> **Note:** Make sure all PHP extensions are installed and enabled before proceeding with the installation. You can check your PHP configuration by running php -m in your terminal.

## Get Started

1. In your terminal, navigate to the www folder
Windows: cd your\www\folder
Linux/Mac: cd your/www/folder
2. Initialize Saashovel
Clone the SaaShovel repository (or download it from GitHub). You will need to generate a PAT (Personal Access Token). More information on how to generate it can be found here.

```
git clone https://github.com/tcja/saashovel.git
```

Navigate to the SaaShovel folder

```
cd saashovel
```

Copy the ".env.example" file and rename it to ".env" to configure your app. More information is provided below in point 5.

Windows: copy .env.example .env
Linux/Mac: cp .env.example .env
Install PHP dependencies

```
composer install
```

Install Node.js dependencies

```
npm install
```

Then

```
php artisan saashovel:ignite
```

This command will:

Generate application encryption key → php artisan key:generate
Set up database with initial data → php artisan migrate --seed
4. Start your development server
Change the host url in the "vite.config.js" file to your local dev url.

Then
```
npm run dev
```

or
```
php artisan saashovel:dev
```

Finally

```
php artisan serve
```

5. Configure your application
### Environment Variables

Update your .env file with the following settings:

### Essential Settings

Basic Configuration:
```
APP_NAME - Your application name
APP_URL - Your application's base URL
APP_THEME - Default themes (light/dark/sunset/nature)
```

Localization:
```
APP_LOCALE - Default language
APP_AVAILABLE_LOCALES - Supported languages (comma-separated)
APP_USE_BROWSER_LOCALE - Enable automatic language detection
```

### Payment Gateway Credentials

Select your provider: BILLING_PROVIDER (stripe/paddle/lemonsqueezy/nowpayments)
### Stripe Configuration

```
STRIPE_KEY - Publishable key from Stripe dashboard
```

Get it here: https://dashboard.stripe.com/test/apikeys (Publishable key)
```
STRIPE_SECRET - Secret key from Stripe dashboard
```

Get it here: https://dashboard.stripe.com/test/apikeys (Secret key)
```
STRIPE_WEBHOOK_SECRET - Webhook signing secret
```

Get it here: https://dashboard.stripe.com/test/webhooks (Signing secret)
### Paddle Configuration

```
PADDLE_SANDBOX - Set to true for test mode
PADDLE_VENDOR_ID - Your Paddle vendor ID
```

Get it here: https://sandbox-vendors.paddle.com (click on the three dots "..." at the top left of the page then you'll see the vendor ID on: "Seller ID")
```
PADDLE_VENDOR_AUTH_CODE - API authentication code
```

Get it here: https://sandbox-vendors.paddle.com/authentication-v2 (+Generate API KEY)
```
PADDLE_PUBLIC_KEY - Public key for verification
```

Get it here: https://sandbox-vendors.paddle.com/authentication-v2 (Default)
```
PADDLE_CLIENT_SIDE_TOKEN - Client-side token
```

Get it here: https://sandbox-vendors.paddle.com/authentication-v2 (+Generate client-side token)
```
PADDLE_WEBHOOK_SECRET - Webhook signing secret
```

Get it here: https://sandbox-vendors.paddle.com/notifications-v2 (+New destination)
### LemonSqueezy Configuration

```
LEMON_SQUEEZY_API_KEY - API key from dashboard
```

Get it here: https://app.lemonsqueezy.com/settings/api
```
LEMON_SQUEEZY_STORE - Your store ID
```

Get it here: https://app.lemonsqueezy.com/settings/stores (#XXXXXX)
```
LEMON_SQUEEZY_SIGNING_SECRET - Webhook signing secret
```

Get it here: https://app.lemonsqueezy.com/settings/webhooks
### NowPayments Configuration

```
NOWPAYMENTS_API_KEY - API key from dashboard
```

Get it here: https://account-sandbox.nowpayments.io/store-settings#keys
```
NOWPAYMENTS_IPN_SECRET - IPN secret for webhooks
```

Get it here: https://account-sandbox.nowpayments.io/store-settings#notifications
```
NOWPAYMENTS_CURRENCY - Default currency for transactions
NOWPAYMENTS_WEBHOOK_PATH - Webhook path for handling callbacks
NOWPAYMENTS_EMAIL - Dashboard login email
NOWPAYMENTS_PASSWORD - Dashboard login password
NOWPAYMENTS_BASE_URL - API base URL (sandbox/production)
```

When in dev mode: https://api-sandbox.nowpayments.io/v1/
### Subscription Tiers

```
FIRST_TIER_SUBSCRIPTION_NAME - Name of your basic tier
SECOND_TIER_SUBSCRIPTION_NAME - Name of your advanced tier
THIRD_TIER_SUBSCRIPTION_NAME - Name of your premium tier
DEFAULT_CURRENCY - Default currency for your pricing
```

The names must strictly match (case-sensitive) the subscription tier names you've set in your billing provider's dashboard.

> **Pro Tip:** For a Step By Step guide on how to create subscription plans, please click here

### Additional Features

```
GOOGLE_ANALYTICS_WIDGETS - Enable analytics in admin panel
COOKIE_CONSENT - Enable GDPR cookie consent
TERMS_AND_PRIVACY_POLICY - Enable legal pages
SEND_EMAIL_CONTACT - Enable contact form emails
SPA_UX - Enable SPA-like experience
```

More configurable features are available in the .env file, each with comments to help you understand their purpose
Remember to never commit your .env file to version control. Keep your API keys and secrets secure!

> **Pro Tip:** Most configuration options can be modified through:

The admin panel under the "My Env." tab for quick access
Environment variables in your .env file for different settings across environments
The config file ("config/saashovel.php") provides defaults and additional documentation.
6. Start customizing
Main folders to customize:

resources/views/components/ - UI components
resources/views/livewire/ - Livewire components
app/Http/Livewire/ - Livewire component logic
app/Filament/ - Admin panel customization
config/saashovel.php - Main configuration
Make sure to review the documentation before making significant changes. Each component is documented with its available props and usage examples.

### Artisan Commands

SaaShovel provides several custom artisan commands to streamline your development workflow:

saashovel:ignite
Initialize your SaaShovel project

```
php artisan saashovel:ignite
```

This command will:

Generate application key
Run database migrations with seeders
saashovel:flush
Reset your application to a clean state

```
php artisan saashovel:flush
```

This command will:

Refresh the database (migrate:fresh --seed)
Clear all application caches (optimize:clear)
> **Pro Tip:** Use saashovel:flush during development to quickly reset your application state. Be careful not to use it in production as it will erase all data!

saashovel:page
Generate a new Livewire page component with proper structure

```
php artisan saashovel:page {name}
```

This command will create:

```
A new Livewire component in app/Livewire/Page/{Name}/{Name}.php
A corresponding view file in resources/views/livewire/pages/{name}/{name}.blade.php
# Example usage
php artisan saashovel:page About
```

saashovel:emptyPlans
Delete all subscription plans from the database (useful for a plan data refresh)

```
php artisan saashovel:emptyPlans
```

This command will:

Ask for confirmation before proceeding
Remove all records from the subscription_plans table
saashovel:dev
Set up application for development mode

```
php artisan saashovel:dev
```

This command will:

Backup your .env file
Update environment settings for local development
Clear all application caches (optimize:clear)
Reset and seed the database (migrate:fresh --seed)
Prepare Vite development server
> **Pro Tip:** After running saashovel:dev, don't forget to start the Vite development server with npm run dev. Review the development checklist to ensure everything is properly configured.

saashovel:prod
Deploy application to production mode

```
php artisan saashovel:prod
```

This command will:

Backup your .env file
Update environment settings for production
Clear all application caches (optimize:clear)
Install production dependencies (composer install --no-dev)
Optimize autoloader and cache configuration
Optimize Filament components and icons
Build production assets (npm run build)
Run database migrations
> **Pro Tip:** Use saashovel:prod when deploying to production. Make sure to review the post-deployment checklist displayed after completion. Always test in a staging environment first!

## Billing Providers

SaaShovel supports multiple payment processors, configurable via the BILLING_PROVIDER environment variable.

### Supported Providers

### Stripe

### LemonSqueezy

### Paddle

NOWPayments (Cryptocurrency)
### Payment Configuration

### Hybrid Payment Setup

Configure multiple payment methods by:

Setting your primary provider (e.g., BILLING_PROVIDER=paddle)
Adding NOWPayments API credentials for additional crypto payment options
The "Pay with Crypto" button will appear below the standard payment button
### Crypto-Only Setup

For exclusive cryptocurrency payments, set BILLING_PROVIDER=nowpayments

### Subscription Management

SaaShovel automatically handles the entire subscription process. Users can manage their subscriptions through:

Stripe: Customer portal access via dashboard button
LemonSqueezy: Customer portal access via dashboard button
Paddle: Built-in customer portal
NOWPayments: Built-in customer portal
All providers include a "Cancel Plan" button for easy subscription cancellation.

Features:

Automatic plan data synchronization
Built-in subscription management
Flexible payment options
User-friendly dashboard integration
> **Note:** For pricing plan design customization, please refer to the Components section of this documentation.

### Implementation Steps

Set up subscription plans in your chosen provider's dashboard (see below for detailed steps).
Configure API credentials in your .env file, ensuring all necessary variables are set.
Ensure plan names in your .env file match exactly with your provider's dashboard.
SaaShovel will automatically fetch and display plan details.
### Setting Up Subscription Plans

### Stripe

Sign in to your Stripe Dashboard.
Click on the toggle button in the top right to switch to Test mode.
In the sidebar, go to Product catalog (or click here).
Click the + Create product button in the top right.
In the "Create a product" form:
Enter the Name matching your FIRST_TIER_SUBSCRIPTION_NAME, SECOND_TIER_SUBSCRIPTION_NAME, or THIRD_TIER_SUBSCRIPTION_NAME
Add an optional description and images
Choose Recurring price type
Set your price and billing interval (monthly/yearly)
Click More pricing options
Enter the Name of the plan (same as first step) in the Price description
Click Next
Click Add product
Repeat the process for each subscription tier.
Setup the customer's portal by clicking here
Go to Subscriptions → Toggle on "Customer can switch plans"
Add the plans you created by typing their name, this will allow your customers to update their plan
Customize the rest of the customer portal as you wish
For API keys:
Go to Developers → API keys in the Search field (or click here)
Copy the Publishable key to STRIPE_KEY in your .env
Reveal and copy the Secret key to STRIPE_SECRET
For Webhooks:
For Stripe, you can use the Stripe CLI to forward events to your local server
Or Alternatively, go to Developers → Webhooks (or click here)
Click + Add endpoint
Enter your application's webhook URL (the default end point is "/stripe/webhook")
Select the events to listen for (typically customer.subscription.* events)
Copy the generated Signing secret to STRIPE_WEBHOOK_SECRET in your .env
### LemonSqueezy

Sign in to your LemonSqueezy Dashboard.
In the sidebar, go to Store → Products (or click here).
Click the + New product button.
In the "Add Product" form:
Enter the Name matching your FIRST_TIER_SUBSCRIPTION_NAME, SECOND_TIER_SUBSCRIPTION_NAME, or THIRD_TIER_SUBSCRIPTION_NAME
Select Subscription as the product type
Select Standard pricing as the Pricing model
Add description and media (optional)
Set your price and billing interval (monthly/yearly)
Configure trial period if needed
Set up subscription features and limits
Click Publish product
Repeat the process for each subscription tier.
Setup the customer's portal by clicking here
Toggle on "Enable customer portal"
Go to Subscriptions → Toggle on "Cancel subscriptions" and "Update subscriptions"
Add the plans you created, this will allow your customers to update their plan
Customize the rest of the customer portal as you wish
For API setup:
Go to Settings → API (or click here)
Generate a new API key if needed
Copy the key to LEMON_SQUEEZY_API_KEY in your .env
For Store ID:
Go to Settings → Stores (or click here)
Copy your Store ID (format: #XXXXXX) without the "#"
Set it as LEMON_SQUEEZY_STORE in your .env
For Webhooks:
Go to Settings → Webhooks (or click here)
Click + button
Enter your application's webhook URL (the default end point is "/lemon-squeezy/webhook")
Select the following events to monitor:
order_created
subscription_created
subscription_updated
subscription_cancelled
subscription_expired
subscription_payment_failed
subscription_payment_success
subscription_plan_changed
Click Save Webhook
Copy the generated Signing Secret to LEMON_SQUEEZY_SIGNING_SECRET in your .env
### Paddle

Sign in to your Paddle Sandbox Dashboard.
For Products setup:
Go to Checkout → Website Approval (or click here)
Click + Add a new domain
```
Add your local test domain (e.g., myapp.test); it will be automatically approved.
```

Go to Catalog → Products (or click here)
Click + New Product
Enter product name
Click Save
Click + New price
Enter price details:
Choose Recurring price type
Enter the Name matching your FIRST_TIER_SUBSCRIPTION_NAME, SECOND_TIER_SUBSCRIPTION_NAME, or THIRD_TIER_SUBSCRIPTION_NAME
Enter the same Name in the Internal description
Set your price and billing interval (monthly/anually)
Configure trial period if needed
Click Save
Repeat for each subscription tier
For API credentials:
Go to Developer Tools → Authentication (or click here)
Copy your Seller ID to PADDLE_VENDOR_ID
Generate and copy API Key to PADDLE_VENDOR_AUTH_CODE
Copy "Default" Key to PADDLE_PUBLIC_KEY
Generate and copy Client-Side Token to PADDLE_CLIENT_SIDE_TOKEN
For Webhooks:
Go to Developer Tools → Notifications (or click here)
Click + New destination
Enter a Description
Enter your application's webhook URL (the default end point is "/paddle/webhook")
Select the following events to monitor:
transaction.completed
transaction.updated
subscription.canceled
subscription.created
subscription.paused
subscription.updated
customer.created
customer.updated
Click Save destination
Click on your newly created Webhook (the three dots)
Click on Edit destination
Copy the Secret Key to PADDLE_WEBHOOK_SECRET
For sandbox testing:
Set PADDLE_SANDBOX=true in your .env
Use test card details from Paddle's documentation
### NOWPayments

Sign in to your NOWPayments Sandbox account
For Subscriptions setup:
In the sidebar, go to Payment Tools → Subscriptions (or click here).
Click Create subscription plan
Enter the Name matching your FIRST_TIER_SUBSCRIPTION_NAME, SECOND_TIER_SUBSCRIPTION_NAME, or THIRD_TIER_SUBSCRIPTION_NAME
Choose 1 Month(s) as the period duration (this will be a monthly subscription)
Set your price
Click + Advanced settings
For Payment notifications link: Enter your application's webhook URL (the default end point is "/nowpayments/webhook")
For Successful payment page, Payment failed page and Partial payment page: enter the dashboard route (e.g. my-app.test/dashboard) as to redirect the customer to its dashboard once the payment is made
Click Create product
Repeat for each subscription tier
API Configuration:
Use credentials (the same ones from your Nowpayment's Dashboard) from your .env:
Email: NOWPAYMENTS_EMAIL
Password: NOWPAYMENTS_PASSWORD
Go to Settings → Payments → Payout wallets (or click here)
Add your payout wallet
Go to Settings → Payments → API Keys (or click here)
Generate a new API key
Copy the API Key to NOWPAYMENTS_API_KEY
Go to Settings → Payments → Payment details (or click here)
Choose your desired payment details
Webhook Setup:
Go to Settings → Payments → Instant payment notifications (or click here)
Copy the IPN Secret Key to NOWPAYMENTS_IPN_SECRET
Enter your application's webhook URL
Environment Settings:
Set your preferred currency in NOWPAYMENTS_CURRENCY (e.g., USD)
For sandbox testing, set:
```
NOWPAYMENTS_BASE_URL=https://api-sandbox.nowpayments.io/v1/
```

Use test cryptocurrencies for payments
### Webhook Management

Webhook listeners are located in the app/Listeners/ directory.

### Provider Implementations

Stripe & Paddle:
Handled through Laravel's Cashier package.

LemonSqueezy:
Implemented using the LemonSqueezy Laravel package.

NOWPayments:
Managed by SaaShovel's proprietary package (tcja/nowpayments-laravel).

### Testing Webhooks Locally

Use Ngrok (free tier with limits)
Or use LocalTunnel (completely free)
These tools create a secure tunnel to your local environment for testing webhooks
Alternatively, for Stripe, you can use the Stripe CLI to forward events to your local server
Stripe also offers a Webhook Tester in their dashboard
Other providers may offer similar webhook testing tools in their dashboards
See the logs from the webhooks in Laravel's log storage at storage/logs/laravel.log
### Billing Provider Flexibility

SaaShovel provides flexibility in changing billing providers without service interruption.

### Emergency Provider Switch

In case of billing provider issues (e.g., account suspension), you can:

Change BILLING_PROVIDER to an alternative provider.
Transfer existing users to the new provider either by:
Having users create new accounts.
Using SQL to update existing user billing providers.
Switch back to the original provider when issues are resolved.
### Provider Migration

While the app supports multiple billing providers simultaneously:

Previous subscription data remains intact when switching providers.
New subscriptions will be added to existing records.
The database maintains history from all providers.
> **Note:** While multiple provider support offers flexibility, maintaining subscriptions across different providers may lead to complex database records. Consider consolidating to a single provider (or the hybrid method with NOWPayments) for cleaner data management.

## Layouts

The application uses two main layouts located in resources/views/layouts:

### Dashboard Layout

app.blade.php - This layout is used when users are logged into their dashboard.

### Public Layout

guest.blade.php - This layout is used for:

All visitors
Public pages (even when accessed by logged-in users)
Home page
### Navigation Menu

The navigation menu is implemented in two locations:

resources/views/components/navigation-menu.blade.php (for dashboard layout)
resources/views/components/header.blade.php (for public layout)
### CMS Menu Integration

<!-- Blog menu code -->
```
@php $menu = \LaraZeus\Sky\SkyPlugin::get()->getModel('Navigation')::fromHandle('main'); @endphp
@if($menu && $menu->items)
```

@foreach($menu->items as $item)
```
        {!! \App\CustomRenderNavItem::render($item, $menuLinkClass) !!}
```

@endforeach
@endif
<!-- /Blog menu code -->
This code automatically displays pages created through the CMS. The default menu handle is "main".

### Manual Link Addition

Add links manually below the CMS menu code:

<!-- Site links -->
```
<div class="bg-gray-100 p-4 rounded-md font-mono text-sm mt-2">
    <a href="#features" class="class">Features</a>
    <a href="#pricing" class="class">Pricing</a>
</div>
```

<!-- /Site links -->
> **Note:** When creating menus through the CMS, ensure you use the "main" handle for the menu to display properly, or update the handle in the code if you prefer a different name.

## Localization

### Browser-Based Localization

Saashovel supports automatic locale detection based on browser settings. Configure this in your .env file:

```
APP_USE_BROWSER_LOCALE=true # Enable browser-based locale detection
APP_AVAILABLE_LOCALES=en,es,fr,de,it,tr # Define available locales (only works when APP_USE_BROWSER_LOCALE is true)
```

> **Tip:** Set APP_USE_BROWSER_LOCALE to true to automatically serve content in the user's preferred language.

### Translation Files

The application uses Laravel's standard JSON-based localization system. Locale files are organized in different locations based on their purpose:

### Main Application Translations

resources/lang/
### CMS Translations

resources/lang/vendor/zeus-sky/
### Contact Page Translations

resources/lang/vendor/zeus-wind/
> **Note:** Saashovel comes with multiple language translations out of the box. Make sure to:

Only list actually translated languages in APP_AVAILABLE_LOCALES
Maintain translations in all required locations when adding new text
Keep language files synchronized across all components
## Admin Panel

Users with admin rights are automatically redirected to the admin panel upon login. The panel consists of several tabs, each serving specific administrative functions.
It is powered by the powerful Filament package.

### Dashboard

Features integrated Google Analytics widgets. To enable:

Follow the setup instructions at Filament Google Analytics (starting from the configuration section)
Set GOOGLE_ANALYTICS_WIDGETS=true in your .env file to display widgets
### Users

Comprehensive user management interface for adding, removing, and updating user data.
Impersonate users to assist them with any issues they encounter by clicking on the impersonate icon.

### My Env.

Direct environment variable management interface.

> **Warning:** Modifying critical variables (APP_NAME, APP_KEY) may require re-authentication and could affect application functionality.

### Contact Management

### Departments

Configure contact form departments. The contact form remains functional even without departments.

### Letters

View and manage submitted contact form messages.

Contact page views can be customized at: resources/views/vendor/zeus/themes/zeus/wind

> **Note:** The contact feature is based on https://github.com/lara-zeus/wind. Visit their documentation for more customization information.

### Content Management

### Pages

Create and manage pages with granular permission control. Configure URL prefixes using:

BLOG_URL_PREFIX (must not be empty to avoid auth routing issues)
BLOG_PAGE_URL_PREFIX
Page layout template: resources/views/vendor/zeus/themes/zeus/sky/page.blade.php

### FAQs

Create and manage FAQ pages. Configure URL prefix using BLOG_FAQ_URL_PREFIX.
FAQ layout template: resources/views/vendor/zeus/themes/zeus/sky/addons/faq.blade.php

### Navigations

Create and manage navigation menus.

Tips:

Use "main" as the default menu handle
Create pages before creating menu items for easier page selection
For more details, See here
> **Note:** The CMS feature is based on https://github.com/lara-zeus/sky. By default, the library and tag features are disabled, but you can enable them if needed (in AdminPanelProvider.php). Visit their documentation for more customization information.

## Dashboard Customization

The user dashboard interface is highly customizable through various Livewire components and blade views. SaaShovel automatically loads the appropriate views based on your configured billing provider.

### Main Dashboard

Core dashboard files:

Component: app\Livewire\page\dashboard\Dashboard.php
View: resources\views\livewire\pages\dashboard\dashboard.blade.php
### Subscription Management

Core subscription files:

Component: app\Livewire\page\dashboard\ManageSubscription.php
View: resources\views\livewire\pages\dashboard\manage-subscription.blade.php
### Provider-Specific Views

### Dashboard Views

Located in resources\views\livewire\pages\dashboard\partials\

### LemonSqueezy

lemonsqueezy-manage-subscription.blade.php
lemonsqueezy-price-table.blade.php
### NOWPayments

nowpayments-manage-subscription.blade.php
nowpayments-price-table.blade.php
### Paddle

paddle-manage-subscription.blade.php
paddle-price-table.blade.php
### Stripe

stripe-manage-subscription.blade.php
stripe-price-table.blade.php
### Landing Page Views

Located in resources\views\livewire\pages\landing-page\partials\

lemonsqueezy-price-table.blade.php
nowpayments-price-table.blade.php
paddle-price-table.blade.php
stripe-price-table.blade.php
> **Note:** All views are automatically loaded based on your BILLING_PROVIDER environment variable setting. No additional configuration is required.

## App Customization

### Service Provider Configuration

The AppServiceProvider (app/Providers/AppServiceProvider.php) handles core application configurations, including billing, themes, webhooks, and component registration.

### Key Features

Billing trait selection
Theme service registration
Custom Blade directives (@theme)
Webhook handling for Stripe and Paddle
Component registration for auth elements
Custom contact form binding
> **Note:** When modifying the AppServiceProvider, ensure to:

Maintain webhook routes if using Stripe or Paddle
Keep component registrations synchronized with your views
Update the AdminPanelProvider when changing hidden resources
### Authentication Screens

The authentication screens can be customized through the DevDojo Auth package setup interface at myapp.test/auth/setup. Full documentation available at DevDojo Auth Docs.

> **Note:** The setup interface is automatically disabled in production environment.

## Admin Panel

Filament admin panel can be customized in app/Providers/Filament/AdminPanelProvider.php. Refer to Filament documentation for detailed customization options.

### Cookie Consent

Cookie consent banner can be customized through:

Views: resources/views/vendor/cookie-consent
Service Provider: app/Providers/CookiesServiceProvider.php
See documentation for more details.
### Contact Page

The contact page can be managed through the Admin Panel's Contact tab:

Departments: Create departments to categorize incoming messages (optional)
Letters: View and manage submitted contact form messages
Views location: resources/views/vendor/zeus/themes/zeus/wind
Notes:

Set SEND_EMAIL_CONTACT=true to receive email notifications for new contact submissions
To disable the contact form, comment out the $contact line in the plugins() method of app/Providers/Filament/AdminPanelProvider.php
### FAQ Page

Create and manage FAQs through the Admin Panel's Site tab > FAQs sub-tab.
The FAQ view template is located at: resources/views/vendor/zeus/themes/zeus/sky/addons/faq.blade.php

Additional Resources:

Laravel Documentation
Livewire Documentation
Filament Documentation
Jetstream Documentation
## Components

This is a list of SaaShovel components that you can copy and paste to quickly build a landing page.

Since SaaShovel is built ontop of Jetstream, you can also use their components by referring to their documentation here.

All components are located in the folder: resources/views/components/

You can customize each component by either using the attributes or modify the component's source code.

### Header

### Hero Section

### CTA Button

### Toggle Button

### Custom Modal

### Interactive Features Section

### Features Section

### Vertical Feature Section

### Features Grid

### Pricing Section

### FAQ Section

Testimonials Section
### CTA Section

### Footer

### Header

A responsive header component with navigation menu and user authentication options.

Props:
Various styling props for customizing colors and appearance.
Usage:
```
<x-header />
```

Demo:
### Hero Section

A prominent hero section typically used at the top of a landing page.

Props:
title: The main headline text.
subtitle: A supporting subheadline text (supports HTML).
ctaText: Text for the call-to-action button.
ctaUrl: URL for the CTA button.
titleColor: Color of the main headline (defaults to theme setting).
subtitleColor: Color of the subheadline (defaults to theme setting).
ctaBackgroundColor: Background color of the CTA button (defaults to theme setting).
ctaTextColor: Text color of the CTA button (defaults to theme setting).
ctaHoverBackgroundColor: Hover background color of the CTA button (defaults to theme setting).
bgColor: Background color of the hero section (defaults to theme setting).
Usage:
```
<x-hero-section
    title="Welcome to Our Platform"
    subtitle="The best solution for your business needs"
    ctaText="Get Started"
    ctaUrl="/signup"
>
    <x-slot name="image">
        <img src="https://saashovel.com/logos/shovel.png" alt="Hero Image">
    </x-slot>
</x-hero-section>
```

Demo:
Welcome to Our Platform
The best solution for your business needs

## Get Started

Hero Image
### CTA Button

The CTA (Call to Action) Button component is a versatile centered button that can be used for various actions on your website.

Props:
text: The text displayed on the button (default: 'Get Started').
class: CSS classes for styling the button (default: 'text-white bg-lime-600 hover:bg-lime-700').
wire: Livewire method to be called on click (optional).
alpine: URL to redirect to when clicked (optional).
Usage:
```
<x-cta-button
    text="Sign Up Now"
    class="text-white bg-blue-500 hover:bg-blue-600"
/>
```

Demo:
### Toggle Button

A button component that toggles between two states, often used to show/hide content.

Props:
showText: Text displayed when content is hidden (defaults to 'See More...').
hideText: Text displayed when content is shown (defaults to 'Hide Sections').
isShowing: Initial state of the toggle (defaults to false).
class: CSS classes for styling the button (defaults to theme setting).
clickInView: Automatically triggers click when button enters viewport (defaults to false).
Usage:
```
<div x-data="{ showSections: false }">
    <x-toggle-button
        x:is-showing="showSections"
        @toggle-sections.window="showSections = $event.detail"
    />

    <x-features-section x:show-sections="showSections">

        <x-feature
            id="cms"
            title="Powerful Built-in CMS"
            description="Manage your content effortlessly with the integrated Content Management System. Create, edit, and organize your pages with ease."
            media-type="video"
            media-src="illustrations/cms.mp4"
            media-position="right">

            <li>Intuitive page builder</li>
            <li>Custom page permissions</li>
            <li>SEO optimization tools</li>
            <li>Media library management</li>
            <li>Contact page</li>

        </x-feature>

        <x-feature
            id="admin-panel"
            title="Comprehensive Admin Panel"
            description="Take control of your SaaS with the feature-rich admin panel. Monitor performance, manage users, and make data-driven decisions."
            media-type="video"
            media-src="illustrations/admin.mp4"
            media-position="left">

            <li>Google Analytics integration</li>
            <li>User management</li>
            <li>.Env config to customize features</li>
            <li>Contact feature</li>
            <li>CMS features</li>
            <li>Customizable dashboard</li>

        </x-feature>

        <x-feature
            id="auth-screens"
            title="Modern Authentication Screens"
            description="Provide a seamless onboarding experience with the sleek and secure authentication screens."
            media-type="video"
            media-src="illustrations/auth.mp4"
            media-position="right">

            <li>Social login integration</li>
            <li>Two-factor authentication</li>
            <li>Email confirmation functionality</li>
            <li>Password reset functionality</li>
            <li>Customizable design</li>

        </x-feature>

    </x-features-section>
</div>
```

Demo:
See More...
### Custom Modal

A flexible modal component that can be used for various purposes such as alerts, confirmations, or forms.

Props:
id: Unique identifier for the modal (defaults to 'modal').
maxWidth: Maximum width of the modal ('sm', 'md', 'lg', 'xl', '2xl') (defaults to '2xl').
bgColor: Background color of the modal (defaults to theme setting).
textColor: Text color of the modal content (defaults to theme setting).
overlayColor: Color of the modal overlay (defaults to theme setting).
overlayOpacity: Opacity level of the overlay (defaults to theme setting).
titleSize: Font size of the modal title (defaults to 'text-lg').
titleWeight: Font weight of the title (defaults to 'font-medium').
footerBgColor: Background color of the modal footer (defaults to theme setting).
confirmBtnBgColor: Background color of the confirm button (defaults to theme setting).
confirmBtnHoverBgColor: Hover background color of the confirm button (defaults to theme setting).
confirmBtnTextColor: Text color of the confirm button (defaults to theme setting).
cancelBtnBgColor: Background color of the cancel button (defaults to theme setting).
cancelBtnHoverBgColor: Hover background color of the cancel button (defaults to theme setting).
cancelBtnTextColor: Text color of the cancel button (defaults to theme setting).
cancelBtnBorderColor: Border color of the cancel button (defaults to theme setting).
Usage:
```
<x-custom-modal id="login-modal" maxWidth="md">
    <x-slot name="title">
        Login
    </x-slot>

    <x-slot name="content">
        <!-- Login form content -->
        <form class="space-y-4">
            <div>
                <label for="email" class="block text-sm font-medium text-gray-700">
                    Email
                </label>
                <input
                    type="email"
                    id="email"
                    class="mt-1 block w-full rounded-md border-gray-300 shadow-sm"
                />
            </div>

            <div>
                <label for="password" class="block text-sm font-medium text-gray-700">
                    Password
                </label>
                <input
                    type="password"
                    id="password"
                    class="mt-1 block w-full rounded-md border-gray-300 shadow-sm"
                />
            </div>
        </form>
    </x-slot>

    <x-slot name="footer">
        <button
            type="button"
            class="bg-blue-600 text-white px-4 py-2 rounded-md hover:bg-blue-700"
            @click="confirm"
        >
            Login
        </button>

        <button
            type="button"
            class="mr-3 bg-white text-gray-700 px-4 py-2 rounded-md border hover:bg-gray-50"
            @click="close"
        >
            Cancel
        </button>
    </x-slot>
</x-custom-modal>
<button type="button" class="bg-blue-600 text-white px-4 py-2 rounded-md"
    @click="$dispatch('open-modal', { title: 'Login to Your Account', confirmButtonText: 'Login', confirmAction: () =>
        { console.log('Login attempted'); return true; } })">
    Open Modal
</button>
```

Demo:
Open Modal
### Interactive Features Section

A section component that displays features in an interactive tabbed interface.

Props <x-interactive-features-section>:
id: Unique identifier for the section.
title: The main title of the section.
description: A brief description of the features.
bgColor: Background color of the section (defaults to theme setting).
titleColor: Color of the section title (defaults to theme setting).
descriptionColor: Color of the section description (defaults to theme setting).
tabTextColor: Color of the tab text (defaults to theme setting).
activeTabIconColor: Color of the active tab icon (defaults to theme setting).
tabIconColor: Color of inactive tab icons (defaults to theme setting).
Props for <x-interactive-feature-tab>:
name: The name of the tab.
tabId: Unique identifier for the tab.
icon: SVG content for the tab icon.
mediaType: Type of media to display ('image' or 'video') (defaults to empty).
mediaUrl: URL for the media content (defaults to empty).
title: Title of the tab content (defaults to empty).
description: Description text for the tab (defaults to empty).
features: Array of feature points to display with checkmarks (defaults to empty array).
checkmarkColor: Color of the feature checkmark icons (defaults to theme setting).
Usage:
```
<x-interactive-features-section
    id="features"
    title="Unleash the potential of your SaaS"
    description="Don't let technical debt bury your SaaS before it begins. SaaShovel provides the robust foundation you need - from user logins to payment processing. Construct your dream SaaS on solid ground and reach profitability faster."
>
    <x-interactive-feature-tab
        tabId="payments"
        name="Payments"
        icon='
        <svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z"/>
        </svg>'
        title="Multi-Payment Support"
        description="Integrate multiple payment processors for business continuity and flexibility:"
        :features="[
            '<img src=\'https://saashovel.com/logos/stripe.png\' alt=\'Stripe\' class=\'inline mx-1\'><a class=\'font-bold\' href=\'https://stripe.com\' target=\'_blank\' rel=\'noopener noreferrer\'>Stripe</a>',
            '<img src=\'https://saashovel.com/logos/lemonsqueezy.png\' alt=\'LemonSqueezy\' class=\'inline mx-1\'><a class=\'font-bold\' href=\'https://www.lemonsqueezy.com\' target=\'_blank\' rel=\'noopener noreferrer\'>LemonSqueezy</a>',
            '<img src=\'https://saashovel.com/logos/paddle.png\' alt=\'Paddle\' class=\'inline mx-1\'><a class=\'font-bold\' href=\'https://paddle.com\' target=\'_blank\' rel=\'noopener noreferrer\'>Paddle</a>',
            '<img src=\'https://saashovel.com/logos/nowpayments.png\' alt=\'NowPayments\' class=\'inline mx-1\'><a class=\'font-bold\' href=\'https://nowpayments.io\' target=\'_blank\' rel=\'noopener noreferrer\'>NowPayments</a> for crypto'
        ]"
    >
        <p class="mt-2">
            Never worry about payment processor bans again.
        </p>
    </x-interactive-feature-tab>

    <x-interactive-feature-tab
        tabId="subscription"
        name="Subscriptions"
        mediaType="video"
        mediaUrl='illustrations/subscription.mp4'
        icon='
        <svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 5v2m0 4v2m0 4v2M5 5a2 2 0 00-2 2v3a2 2 0 110 4v3a2 2 0 002 2h14a2 2 0 002-2v-3a2 2 0 110-4V7a2 2 0 00-2-2H5z"/>
        </svg>'
        title="Effortless Subscription Journey"
        description="Experience a smooth, end-to-end subscription process:"
        :features="[
            'One-click plan selection',
            'Streamlined user registration',
            'Webhook handling'
        ]"
    >
    </x-interactive-feature-tab>

    <x-interactive-feature-tab
        tabId="permissions"
        name="Permissions"
        mediaType="image"
        mediaUrl='illustrations/permissions.png'
        icon='
        <svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"/>
        </svg>'
        title="Smooth Permission Handling"
        description="Effortlessly manage user access with the powerful and flexible permission system:"
        :features="[
            '<b>@can</b> and <b>@cannot</b> directives to restrict access',
            '<b>$user->can()</b> and <b>$user->cannot()</b> methods for granular control',
            'Route <b>middlewares</b> to restrict access to specific subscriber tiers'
        ]"
    >
    </x-interactive-feature-tab>

</x-interactive-features-section>
```

Demo:
Unleash the potential of your SaaS
Don't let technical debt bury your SaaS before it begins. SaaShovel provides the robust foundation you need - from user logins to payment processing. Construct your dream SaaS on solid ground and reach profitability faster.

Payments

Subscriptions

## Permissions

Multi-Payment Support
Integrate multiple payment processors for business continuity and flexibility:

StripeStripe
LemonSqueezyLemonSqueezy
PaddlePaddle
NowPaymentsNowPayments for crypto
Never worry about payment processor bans again.

### Features Section

A section component to showcase specific features with text and media.

Props for <x-features-section>:
showSections: Controls visibility of the sections (defaults to false).
Props for <x-feature>:
id: Unique identifier for the section.
title: The main title of the feature.
description: A brief description of the feature.
mediaType: Type of media to display ('image', 'video', 'emoji') (defaults to 'image').
mediaSrc: Source URL or content for the media (defaults to empty string).
mediaPosition: Position of the media ('left' or 'right') (defaults to 'right').
bgColor: Background color of the section (defaults to theme setting).
titleColor: Color of the title text (defaults to theme setting).
descriptionColor: Color of the description text (defaults to theme setting).
listItemColor: Color of the list items (defaults to theme setting).
ctaText: Text for the call-to-action button (defaults to null).
ctaUrl: URL for the call-to-action button (defaults to '#').
ctaBgColor: Background color of the CTA button (defaults to theme setting).
ctaTextColor: Text color of the CTA button (defaults to theme setting).
ctaHoverBgColor: Hover background color of the CTA button (defaults to theme setting).
Usage:
```
<x-features-section>
    <x-feature
        id="benefits"
        title="Launch Your SaaS Faster"
        description="Our starter-kit is designed to help you build and launch your SaaS product for a worldwide audience in record time. Focus on your unique features while we handle the details."
        media-type="emoji"
        media-src="💨"
        media-position="right"
        cta-text="Get Started"
        cta-url="#"
    >
        <li>Multiple payment processors for business continuity</li>
        <li>Crypto payments support for a wider audience</li>
        <li>Built-in localization for global reach</li>
        <li>CMS with flexible page permissions</li>
        <li>Admin panel with Google Analytics integration</li>
        <li>Modern auth screens with social provider support</li>
        <li>Configurable features and components to fit your needs</li>
    </x-feature>
</x-features-section>
```

Demo:
Launch Your SaaS Faster
Our starter-kit is designed to help you build and launch your SaaS product for a worldwide audience in record time. Focus on your unique features while we handle the details.

Multiple payment processors for business continuity
Crypto payments support for a wider audience
Built-in localization for global reach
CMS with flexible page permissions
Admin panel with Google Analytics integration
Modern auth screens with social provider support
Configurable features and components to fit your needs
## Get Started

💨

### Vertical Feature Section

A vertically oriented feature section component.

Props:
id: Unique identifier for the section.
title: The main title of the feature.
description: A brief description of the feature.
mediaType: Type of media to display ('video', 'image', or 'emoji') (defaults to empty).
mediaSrc: Source URL or content for the media (defaults to empty).
bgColor: Background color of the section (defaults to theme setting).
titleColor: Color of the title text (defaults to theme setting).
descriptionColor: Color of the description text (defaults to theme setting).
listItemColor: Color of the list items (defaults to theme setting).
ctaText: Text for the call-to-action button (defaults to null).
ctaUrl: URL for the CTA button (defaults to '#').
ctaBgColor: Background color of the CTA button (defaults to theme setting).
ctaTextColor: Text color of the CTA button (defaults to theme setting).
ctaHoverBgColor: Hover background color of the CTA button (defaults to theme setting).
Usage:
```
<x-vertical-feature-section
    id="payment-gateways"
    title="Flexible Payment Options"
    description="SaaShovel supports multiple payment gateways, allowing you to easily bill your users through various methods and expand your payment capabilities."
>
    <li class="list-none">
        <div class="w-full my-7">
            <a class="font-bold" href="https://paddle.com" target="_blank" rel="noopener noreferrer">
                <img src="illustrations/paddle.png" alt="paddle" class="w-1/2 m-auto">
            </a>
        </div>
        SaaShovel supports Paddle as a subscription payment gateway, allowing you to easily bill your users on a monthly, yearly, or per-seat basis. (Customer portal built-in)
    </li>
    <li class="list-none">
        <div class="w-full my-7">
            <a class="font-bold" href="https://stripe.com" target="_blank" rel="noopener noreferrer">
                <img src="illustrations/stripe.png" alt="stripe" class="w-1/3 m-auto">
            </a>
        </div>
        SaaShovel also offers support for Stripe as a subscription gateway, allowing for recurring payments, per-seat pricing, and much more. (Customer portal through Stripe)
    </li>
    <li class="list-none">
        <div class="w-full my-7">
            <a class="font-bold" href="https://lemonsqueezy.com" target="_blank" rel="noopener noreferrer">
                <img src="illustrations/lemonsqueezy.png" alt="lemonsqueezy" class="w-1/2 m-auto">
            </a>
        </div>
        SaaShovel integrates with LemonSqueezy, providing an additional payment processing option for your SaaS business. (Customer portal through LemonSqueezy)
    </li>
    <li class="list-none">
        <div class="w-full my-7">
            <a class="font-bold" href="https://nowpayments.io" target="_blank" rel="noopener noreferrer">
                <img src="illustrations/nowpayments.png" alt="nowpayments" class="w-1/2 m-auto">
            </a>
        </div>
        With NowPayments integration, SaaShovel allows you to accept cryptocurrency payments, expanding your customer base to crypto enthusiasts. (Customer portal built-in)
    </li>
</x-vertical-feature-section>
```

Demo:
Flexible Payment Options
SaaShovel supports multiple payment gateways, allowing you to easily bill your users through various methods and expand your payment capabilities.

paddle
SaaShovel supports Paddle as a subscription payment gateway, allowing you to easily bill your users on a monthly, yearly, or per-seat basis. (Customer portal built-in)
stripe
SaaShovel also offers support for Stripe as a subscription gateway, allowing for recurring payments, per-seat pricing, and much more. (Customer portal through Stripe)
lemonsqueezy
SaaShovel integrates with LemonSqueezy, providing an additional payment processing option for your SaaS business. (Customer portal through LemonSqueezy)
nowpayments
With NowPayments integration, SaaShovel allows you to accept cryptocurrency payments, expanding your customer base to crypto enthusiasts. (Customer portal built-in)
### Features Grid

A grid layout component for displaying multiple feature items.

Props <x-features-grid>:
title: The title of the features section (defaults to 'Why Choose SaaShovel?').
bgColor: Background color of the section (defaults to theme setting).
titleColor: Color of the section title (defaults to theme setting).
gridCols: CSS classes for grid column layout (defaults to 'md:grid-cols-3').
Props for <x-feature-item>:
icon: SVG path for the feature icon.
title: The title of the feature item.
bgColor: Background color of the feature item (defaults to theme setting).
iconColor: Color of the icon (defaults to theme setting).
titleColor: Color of the item title (defaults to theme setting).
contentColor: Color of the item content (defaults to theme setting).
Usage:
```
<x-features-grid title="Skip the foundation, start building your SaaS today">
    <x-feature-item
        icon='
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z">
        </path>
        '
        title="Multi-Payment Support">
        <p>Integrate multiple payment processors:</p>
        <ul class="list-disc pl-5 mt-2">
            <li>
                <img src="http://saashovel.test/logos/stripe.png" alt="Stripe" class="inline mx-1">
                <a class="font-bold" href="https://stripe.com" target="_blank" rel="noopener noreferrer">
```

### Stripe

```
                </a>
            </li>
            <li>
                <img src="http://saashovel.test/logos/lemonsqueezy.png" alt="LemonSqueezy" class="inline mx-1">
                <a class="font-bold" href="https://www.lemonsqueezy.com" target="_blank" rel="noopener noreferrer">
```

### LemonSqueezy

```
                </a>
            </li>
            <li>
                <img src="http://saashovel.test/logos/paddle.png" alt="Paddle" class="inline mx-1">
                <a class="font-bold" href="https://paddle.com" target="_blank" rel="noopener noreferrer">
```

### Paddle

```
                </a>
            </li>
            <li>
                <img src="http://saashovel.test/logos/nowpayments.png" alt="NowPayments" class="inline mx-1">
                <a class="font-bold" href="https://nowpayments.io" target="_blank" rel="noopener noreferrer">
```

NowPayments
```
                </a>
```

for crypto
```
            </li>
        </ul>
        <p class="mt-2">Never worry about payment processor bans again.</p>
    </x-feature-item>

    <x-feature-item
```

icon='
```
        <rect x="2" y="3" width="20" height="14" rx="2" ry="2" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
        </rect>
        <line x1="2" y1="20" x2="22" y2="20" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
        </line>
        <line x1="6" y1="7" x2="18" y2="7" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
        </line>
        <line x1="6" y1="11" x2="14" y2="11" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
        </line>
        <line x1="6" y1="15" x2="10" y2="15" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
        </line>
```

'
title="Built-in CMS">
```
        <p>Create and manage content with ease. Set page permissions to restrict access to subscribers of specific tiers. Includes customizable contact page for customer interaction and a flexible FAQ section.</p>
    </x-feature-item>

    <x-feature-item
```

icon='
```
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z">
        </path>
```

'
title="TALL Stack Powered">
```
        <p>
```

Leverage the power of
```
            <a class="font-bold text-lime-600 hover:underline" href="https://tailwindcss.com" target="_blank" rel="noopener noreferrer">
```

Tailwind
```
            </a>,
            <a class="font-bold text-lime-600 hover:underline" href="https://alpinejs.dev" target="_blank" rel="noopener noreferrer">
```

Alpine.js
```
            </a>,
            <a class="font-bold text-lime-600 hover:underline" href="https://laravel.com" target="_blank" rel="noopener noreferrer">
```

Laravel
```
            </a>, and
            <a class="font-bold text-lime-600 hover:underline" href="https://livewire.laravel.com" target="_blank" rel="noopener noreferrer">
```

Livewire
```
            </a>
```

for a modern, reactive, and scalable application. As well as
```
            <a class="font-bold text-lime-600 hover:underline" href="https://jetstream.laravel.com" target="_blank" rel="noopener noreferrer">
```

Jetstream
```
            </a>
```

for user's account management and
```
            <a class="font-bold text-lime-600 hover:underline" href="https://filamentphp.com" target="_blank" rel="noopener noreferrer">
```

Filament
```
            </a>
```

for the admin panel.
```
        </p>
    </x-feature-item>
</x-features-grid>
```

Demo:
Skip the foundation, start building your SaaS today
Multi-Payment Support
Integrate multiple payment processors:

Stripe Stripe
LemonSqueezy LemonSqueezy
### Paddle

NowPayments NowPayments for crypto
Never worry about payment processor bans again.

Built-in CMS
Create and manage content with ease. Set page permissions to restrict access to subscribers of specific tiers. Includes customizable contact page for customer interaction and a flexible FAQ section.

TALL Stack Powered
Leverage the power of Tailwind , Alpine.js , Laravel , and Livewire for a modern, reactive, and scalable application. As well as Jetstream for user's account management and Filament for the admin panel.

### Pricing Section

A section component to display multiple pricing plans.

Props <x-pricing-section>:
plans: Array of pricing data (defaults to empty array).
pricingId: Unique identifier for the section (defaults to 'pricing').
class: Additional CSS classes (defaults to 'py-10').
title: The title of the pricing section (defaults to 'Pricing').
bgColor: Background color of the section (defaults to theme setting).
titleColor: Color of the section title (defaults to theme setting).
titleSize: Font size of the title (defaults to 'text-3xl').
titleWeight: Font weight of the title (defaults to 'font-bold').
titleAlignment: Text alignment of the title (defaults to 'text-center').
titleMargin: Margin of the title (defaults to 'mb-8').
Props for <x-pricing-plan>:
name: The name of the pricing plan.
price: The price of the plan.
features: Array of features included in the plan.
highlighted: Boolean to highlight this plan (defaults to false).
ctaBtnText: Text for the main CTA button (defaults to 'Get Started').
ctaSmText: Small text below CTA button (defaults to empty).
ctaAction: URL for the CTA button (defaults to '#').
wireClick: Livewire method to call on click.
alpineClick: Alpine.js method to call on click.
planId: Unique identifier for the plan.
showCtaBtn: Show/hide the CTA button (defaults to true).
showCryptoBtn: Show/hide the crypto payment button (defaults to false).
cryptoBtnText: Text for the crypto button (defaults to 'Pay with Crypto').
cryptoWireClick: Livewire method for crypto button.
cryptoAlpineClick: Alpine.js method for crypto button.
cryptoPlanId: Unique identifier for crypto payment plan.
Usage:
```
<x-pricing-section title="Choose Your Plan">
    <x-pricing-plan
        name="Basic Plan"
        price="$19/month"
        :features="['Up to 10 users', 'Basic support', 'Basic analytics']"
        ctaBtnText="Choose Plan"
    />

    <x-pricing-plan
        name="Advanced Plan"
        price="$39/month"
        :features="[
            'Up to 50 users',
            'Priority support',
            'Advanced analytics',
            'Custom integrations',
        ]"
        highlighted="true"
        ctaBtnText="Choose Plan"
    />

    <x-pricing-plan
        name="Pro Plan"
        price="$99/month"
        :features="[
            'Unlimited users',
            '24/7 support',
            'Enterprise analytics',
            'Custom development',
            'Dedicated account manager',
        ]"
        ctaBtnText="Choose Plan"
    />
</x-pricing-section>
```

Demo:
Choose Your Plan
Basic Plan
Up to 10 users
Basic support
Basic analytics

Choose Plan
Advanced Plan
Up to 50 users
Priority support
Advanced analytics
Custom integrations

Choose Plan
Pro Plan
Unlimited users
24/7 support
Enterprise analytics
Custom development
Dedicated account manager

Choose Plan
### FAQ Section

A container component for grouping FAQ items.

Props for <x-faq-section>:
title: The title of the FAQ section (defaults to 'Frequently Asked Questions').
bgColor: Background color of the FAQ section (defaults to theme setting).
titleColor: Color of the section title (defaults to theme setting).
Props for <x-faq-item>:
question: The question text to be displayed.
answer: The answer text to be displayed.
questionClass: Styling classes for the question text (defaults to theme setting).
answerClass: Styling classes for the answer text (defaults to theme setting).
borderClass: Styling classes for the item border (defaults to theme setting).
Usage:
```
<x-faq-section title="Common Questions">
    <x-faq-item
        question="What is your return policy?"
        answer="Our return policy allows returns within 30 days of purchase."
    />

    <x-faq-item
        question="How do I contact support?"
        answer="You can reach our support team through the contact form or email."
    />
</x-faq-section>
```

Demo:
Common Questions
### Testimonial Section

A flexible testimonial section that displays customer feedback in a responsive grid layout.

Props:
testimonials: Array of testimonial objects containing quote, name, title (optional), and avatar (optional).
sectionTitle: The section heading (defaults to "Testimonials").
bgColor: Background color of the section (defaults to theme setting).
cardBgColor: Background color of testimonial cards (defaults to theme setting).
titleColor: Color of the section title (defaults to theme setting).
quoteColor: Color of the testimonial text (defaults to theme setting).
authorNameColor: Color of author names (defaults to theme setting).
authorTitleColor: Color of author titles (defaults to theme setting).
titleSize: Font size of the section title (defaults to 'text-3xl').
titleWeight: Font weight of the section title (defaults to 'font-bold').
titleMargin: Margin for the section title (defaults to 'mb-12').
Usage:
```
<x-testimonial-section
    section-title="What Our Customers Say"
    :testimonials="[
        [
            'quote' => 'Amazing product that simplified our workflow.',
            'name' => 'John Doe',
            'title' => 'CEO at Company',
            'avatar' => '/path/to/avatar.jpg'
        ],
        [
            'quote' => 'Best solution we\'ve found in the market.',
            'name' => 'Jane Smith',
            'title' => 'Product Manager',
            'avatar' => '/path/to/avatar2.jpg'
        ]
    ]"
/>
```

Demo:
What Our Customers Say
"Amazing product that simplified our workflow."
John Doe
John Doe
CEO at Company
"Best solution we've found in the market."
Jane Smith
Jane Smith
Product Manager
Layout Behavior:
Single testimonial: Centered with optimal width
Two testimonials: Displayed side by side, centered in the container
Three or more testimonials: Responsive grid layout (1 column on mobile, 2 on tablet, 3 on desktop)
### CTA Section

The CTA Section component creates a full-width call-to-action section with customizable content and styling.

Props:
title: The main title of the CTA section.
description: A brief description or subtitle.
ctaText: The text for the call-to-action button.
ctaUrl: The URL for the CTA button.
bgColor: Background color of the section (defaults to theme setting).
imagePosition: Position of the image/video/svg ('left' or 'right', defaults to 'right').
titleColor: Color of the title text (defaults to theme setting).
titleSize: Font size of the title (defaults to 'text-3xl').
titleWeight: Font weight of the title (defaults to 'font-bold').
titleMargin: Margin spacing for the title (defaults to 'mb-4').
descriptionColor: Color of the description text (defaults to theme setting).
descriptionSize: Font size of the description (defaults to 'text-xl').
descriptionMargin: Margin spacing for the description (defaults to 'mb-6').
ctaBgColor: Background color of the CTA button (defaults to theme setting).
ctaTextColor: Text color of the CTA button (defaults to theme setting).
ctaHoverBgColor: Background color of the CTA button on hover (defaults to theme setting).
ctaFontWeight: Font weight of the CTA button text (defaults to 'font-semibold').
ctaRounded: Border radius of the CTA button (defaults to 'rounded-md').
ctaPadding: Padding of the CTA button (defaults to 'px-6 py-3').
ctaTransition: Transition effect for the CTA button (defaults to 'transition duration-300').
sectionPadding: Padding for the entire section (defaults to 'sm:py-12 md:py-16 py-5').
containerMaxWidth: Maximum width of the container (defaults to 'max-w-7xl').
imageSpacing: Spacing between the content and image (defaults to 'md:pl-8').
Usage:
```
<x-cta-section
    title="Join Our Newsletter"
    description="Stay updated with our latest news and offers"
    ctaText="Subscribe Now"
    ctaUrl="/subscribe"
    bgColor="bg-gray-100"
/>
```

Demo:
Join Our Newsletter
Stay updated with our latest news and offers

Subscribe Now
### Footer

A comprehensive footer component with multiple columns for links and information.

Usage:
```
<x-footer />
```

Demo:
SaaShovel
Stop digging, start building!

© 2024 SaaShovel. All rights reserved.

LINKS
Documentation
Support
LEGAL
Privacy Policy
License
## Page Customization

### Creating Pages

Saashovel offers two methods for creating pages:

1. Using the CMS
Create pages through the Filament admin panel's CMS. This method provides a user-friendly interface with a built-in permission system to restrict page access based on subscription tiers.

> **Tip:** The CMS method is recommended for content-focused pages where you need simple subscription-based access control.

> **Note:** The main page template for pages created via CMS can be customized at: resources/views/vendor/zeus/themes/zeus/sky/page.blade.php

2. Using Page Components
Create custom page components using the saashovel:page command for more complex functionality.

```
php artisan saashovel:page {name}
```

This command generates:

```
A Livewire component at app/Livewire/Page/{Name}/{Name}.php
A corresponding Blade view at resources/views/livewire/pages/{name}/{name}.blade.php
# Example usage
php artisan saashovel:page About
```

### Protecting Component-Based Pages

Use the following middleware to restrict access based on subscription tiers:

```
// this route will only be accessible to users with a subscription
Route::get('/your-route-name', YourRouteNameComponent::class)
->middleware(EnsureUserIsSubscribed::class);
// first tier subscribers and above
Route::get('/first-tier-route', FirstTierComponent::class)
->middleware(EnsureUserIsSubscribedToFirstTier::class);
// second tier subscribers and above
Route::get('/second-tier-route', SecondTierComponent::class)
->middleware(EnsureUserIsSubscribedToSecondTier::class);
// third tier subscribers only
Route::get('/third-tier-route', ThirdTierComponent::class)
->middleware(EnsureUserIsSubscribedToThirdTier::class);
```

### Assets Management

Saashovel provides two methods for managing JavaScript assets:

1. Traditional Laravel Assets
For static JavaScript files, use Laravel's standard asset management:

Location: resources/js/
Compile using Vite or your preferred bundler
Import in resources/js/app.js
> **Best Practice:** Use traditional asset management for static JavaScript files that don't require dynamic Blade variables.

2. Dynamic Assets (merged-assets)
For JavaScript that requires Blade variables or dynamic content:

Assets directory: resources/views/livewire/pages/assets/
Main assets files: resources/views/livewire/pages/assets/default-merged-assets.blade.php, resources/views/livewire/pages/assets/merged-assets.blade.php
> **Important:** The default-merged-assets file contains essential code for subscription management. Do not modify it, to add your own assets, do it in the merged-assets file.

### Implementation

The merged assets files are included in both app and guest layouts:

```
@include('livewire.pages.assets.default-merged-assets')
@include('livewire.pages.assets.merged-assets')
```

### When to Use Each Method

Traditional Assets
Static JavaScript files
Third-party libraries
Utility functions
Component behaviors
merged-assets.blade.php
Scripts requiring Blade variables
Dynamic route generation
Payment provider integration
SPA functionality
Other
### Adding Custom Dynamic Assets

To add dynamic assets:

Create your asset file in resources/views/livewire/pages/assets/
Include it in merged-assets.blade.php file:
```
@include('livewire.pages.assets.your-custom-asset')
Best Practice: Always prefer traditional asset management unless you specifically need Blade functionality in your JavaScript code.
```

### Understanding the Home and Landing Pages

The application dynamically displays either the home page or the landing page depending on the user's authentication status:

Logged-in users see: resources/views/livewire/pages/home/home.blade.php
Guests see: resources/views/livewire/pages/landing-page/landing-page.blade.php
### Component Logic

Both the home and landing pages share the same component: app/Livewire/Page/Home/Home.php. This component checks the user's authentication status and loads the appropriate view.

### Permission System

SaaShovel includes a robust permission system to control access to different features based on user roles and subscription tiers.

### Available Permissions

Permission	Access Level
public	Anyone can access
access admin panel	Administrators only
access basic features	Registered users without subscription
access premium features	Any subscribed user
access first tier features	First tier subscribers and above
access second tier features	Second tier subscribers and above
access third tier features	Third tier subscribers only
### System Roles

Role	Assigned Permissions
admin	access admin panel, access basic features, access premium features, access first tier features, access second tier features, access third tier features
user	access basic features
premium-first-tier	access basic features, access premium features, access first tier features
premium-second-tier	access basic features, access premium features, access second tier features
premium-third-tier	access basic features, access premium features, access first tier features, access second tier features, access third tier features
Role Assignment: Upon registration, users are automatically assigned the "user" role with basic feature access. When subscribing to a plan, their role is upgraded to the corresponding tier role (first, second, or third tier). Users can only have one role at a time, though each role may grant multiple permissions.

### Using Permissions

### In Blade Templates

```
@can('access second tier features')
    This is restricted to second-tier and above subscribers.
@endcan

@if(auth()->user()->can('access basic features'))
    Only users who are registered but not subscribed will see this.
@endif
```

### In the page editor

### In the Back-End

```
if (Auth::user()->can('access second tier features')) {
    'Only users who are subscribed to the second tier or higher will access this.'
}
```

### Available Middlewares

```
// this route will only be accessible to users with a subscription
Route::get('/your-route-name', YourRouteNameComponent::class)
->middleware(EnsureUserIsSubscribed::class);
// first tier subscribers and above
Route::get('/first-tier-route', FirstTierComponent::class)
->middleware(EnsureUserIsSubscribedToFirstTier::class);
// second tier subscribers and above
Route::get('/second-tier-route', SecondTierComponent::class)
->middleware(EnsureUserIsSubscribedToSecondTier::class);
// third tier subscribers only
Route::get('/third-tier-route', ThirdTierComponent::class)
->middleware(EnsureUserIsSubscribedToThirdTier::class);
Pro Tip: Permissions are automatically managed based on user subscriptions. When a user upgrades or downgrades their subscription, their permissions are updated accordingly.

Security Note: Always combine frontend permission checks with backend middleware to ensure proper security. Frontend checks are for UI purposes only.
```

## Database & Seeding

### Database Configuration

Thanks to Laravel's database abstraction layer, Saashovel supports multiple database systems out of the box:

mysql (Default)
pgsql (PostgreSQL)
sqlite (SQLite)
sqlsrv (SQL Server)
Configuration Example
```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=your_database
DB_USERNAME=your_username
DB_PASSWORD=your_password
```

### Database Seeding

SaaShovel comes with pre-configured database seeds that set up your application with default roles, permissions, navigation menus, and test users.

### Default Database Configuration

### Roles & Permissions Structure

Role	Assigned Permissions
admin	All permissions
user	access basic features
premium-first-tier	access basic features, premium features, first tier features
premium-second-tier	access basic features, premium features, first & second tier features
premium-third-tier	access basic features, premium features, all tier features
### Default Test Users

Role	Email	Password
admin	admin@admin.com	admin@admin.com
user	user@user.com	user@user.com
### Default Navigation Menu

Name	Handle	Menu Items
main	main	Contact (/contact), Features (/#features), Pricing (/#pricing)
Pro Tips:

You can modify the AdminUserSeeder.php (database/seeders/AdminUserSeeder.php) file to customize default users and roles
Database migrations and seeders work across all supported database systems
Use database transactions for complex seeding operations
Important Notes:

Change default admin credentials in production
While primarily tested with MySQL, other databases should work seamlessly
Always backup your database before major changes
Theme System
SaaShovel includes a flexible theming system that allows you to customize the entire look of your application. Themes are configured in config/themes.php and can be switched using the APP_THEME environment variable.

### Built-in Themes

### Light Theme

```
APP_THEME=light
```

Default light mode with clean, professional styling

### Dark Theme

```
APP_THEME=dark
```

Dark mode optimized for low-light environments

### Sunset Theme

```
APP_THEME=sunset
```

Warm and inviting theme with orange and rose accents

### Nature Theme

```
APP_THEME=nature
```

Organic feel with emerald greens and amber accents

### Theme Structure

Themes are organized by components, each with their own customizable properties:

### Global Settings

Background colors
Text colors
Accent colors
Navigation styles
### Component-Specific Styles

Header & navigation
Hero sections
Feature displays
Pricing tables
Modals & overlays
Interactive elements
### Creating Custom Themes

Add your own theme by extending the themes configuration:

```
// config/themes.php
```

'custom-theme' => [
'global' => [
'bgColor' => 'bg-blue-50',
'textColor' => 'text-blue-900',
'accentColor' => 'text-blue-600',
```
        // ... other global settings
```

],
'header' => [
'bgColor' => 'bg-white',
'menuLinkClass' => 'text-blue-600 hover:text-blue-700',
```
        // ... component specific settings
```

],
```
    // ... other component configurations
```

],
Then activate it by setting:

```
APP_THEME=custom-theme
```

> **Pro Tip:** All color classes are based on Tailwind CSS. You can use any Tailwind color utility class in your custom theme configuration.

> **Note:** After modifying theme configurations, remember to clear your application cache:

```
php artisan config:clear
```

## Security

### Core Security

Essential security configurations in your .env file:

```
APP_ENV=production
APP_DEBUG=false
SESSION_SECURE_COOKIE=true
SESSION_SAME_SITE=lax
```

### CSRF Protection

Laravel and Livewire automatically handle CSRF protection. Every form should include the directive:

```
@csrf
```

### XSS Prevention

Blade automatically escapes content. For raw HTML, use with caution:

```
{{ $escapedContent }}
{!! $rawContent !!}
```

### Livewire Security

Protect sensitive properties using:

#[Locked]
public $sensitiveData;  // Cannot be modified from frontend

```
protected $queryString = ['search' => ['except' => '']]; // URL parameters

// Validate component actions
public function save()
{
    $this->validate([
```

'email' => 'required|email',
'password' => 'required|min:8'
```
    ]);
}
```

### Security Best Practices

Always validate user input using Form Requests
Use prepared statements (Laravel's query builder handles this)
Keep dependencies updated (composer audit)
Set proper file permissions (storage: 775, config: 644)
Use .env for sensitive credentials
Enable HTTP-only cookies
Implement rate limiting on APIs and forms
### Authentication

The application uses Laravel Sanctum for API authentication and session-based auth for web routes.

> **Tip:** Use middleware groups to protect routes:

```
 Route::middleware(['auth:sanctum', 'verified'])->group(...)
```

### Payment Webhook Security

The application verifies webhook signatures for all payment providers (Stripe, Paddle, LemonSqueezy, NOWPayments). This ensures that only legitimate requests from the payment providers are processed:

> **Important:**

Keep webhook secrets secure in .env file
Use HTTPS for webhook endpoints
Configure webhook URLs in provider dashboards
Monitor webhook failures
### File Upload Security

Secure file upload handling:

```
// Validate file uploads
```

'document' => ['required', 'file', 'mimes:pdf,docx', 'max:10240']

```
// Store in private disk
```

Storage::disk('private')->put($path, $file, 'private')
> **Note:** Regular security updates and audits are crucial. Use:

```
composer audit
```

to check for known vulnerabilities in your dependencies.

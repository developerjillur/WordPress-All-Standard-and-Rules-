# CodeCanyon WordPress Plugin Submission Standards & Guidelines

> **Complete Reference Guide for Plugin Authors**
> Last Updated: December 2025

---

## Table of Contents

1. [Overview](#overview)
2. [File Organization & Structure](#file-organization--structure)
3. [Naming Conventions & Prefixing](#naming-conventions--prefixing)
4. [Documentation Requirements](#documentation-requirements)
5. [Review Process](#review-process)
6. [Security Compliance](#security-compliance)
7. [PHP Coding Standards](#php-coding-standards)
8. [JavaScript Standards](#javascript-standards)
9. [CSS Standards](#css-standards)
10. [Asset Loading Requirements](#asset-loading-requirements)
11. [Database Security](#database-security)
12. [WordPress Compatibility](#wordpress-compatibility)
13. [Presentation & Image Requirements](#presentation--image-requirements)
14. [Item Description & Metadata](#item-description--metadata)
15. [Licensing Structure](#licensing-structure)
16. [Revenue Sharing & Earnings](#revenue-sharing--earnings)
17. [Exclusivity Policy](#exclusivity-policy)
18. [Privacy & Legal Compliance](#privacy--legal-compliance)
19. [Prohibited Content](#prohibited-content)
20. [Common Rejection Reasons](#common-rejection-reasons)
21. [Pre-Submission Checklist](#pre-submission-checklist)
22. [Useful Resources](#useful-resources)

---

## Overview

CodeCanyon is Envato's premium marketplace for code items including WordPress plugins. The platform employs a rigorous review process evaluating:

- **Technical Quality**: Code standards, security, and performance
- **Unique Value Proposition**: Differentiation from existing solutions
- **Commercial Viability**: Market demand and practical utility
- **Presentation Quality**: Professional appearance and documentation

### Review Timeline

| Item Type | Typical Review Time |
|-----------|-------------------|
| WordPress Plugins | 1-3 business days |
| Complex Items | May require extended evaluation |

---

## File Organization & Structure

### Required Folder Hierarchy

```
plugin-name/
├── plugin-name.php          # Main plugin file
├── uninstall.php            # Cleanup on uninstall
├── readme.txt               # WordPress readme
├── includes/
│   ├── class-plugin-name.php
│   ├── class-plugin-name-loader.php
│   └── class-plugin-name-i18n.php
├── admin/
│   ├── class-plugin-name-admin.php
│   ├── css/
│   │   └── plugin-name-admin.css
│   ├── js/
│   │   └── plugin-name-admin.js
│   └── partials/
│       └── plugin-name-admin-display.php
├── public/
│   ├── class-plugin-name-public.php
│   ├── css/
│   │   └── plugin-name-public.css
│   ├── js/
│   │   └── plugin-name-public.js
│   └── partials/
│       └── plugin-name-public-display.php
├── languages/
│   └── plugin-name.pot
└── assets/
    └── images/
```

### Critical Rules

| Rule | Requirement |
|------|-------------|
| Root Directory Files | ❌ **PROHIBITED** - Results in automatic rejection |
| Folder Hierarchy | ✅ Logical grouping required |
| Empty Folders | ❌ Remove all empty directories |
| Unused Files | ❌ Remove all unused files |

---

## Naming Conventions & Prefixing

### File Naming Rules

| Format | Example | Status |
|--------|---------|--------|
| Lowercase with hyphens | `class-plugin-name-admin.php` | ✅ Correct |
| CamelCase | `ClassPluginNameAdmin.php` | ❌ Wrong |
| Underscores | `class_plugin_name_admin.php` | ❌ Wrong |

### Prefixing Requirements

**Everything must be prefixed with a unique identifier (minimum 3 characters, recommended 5+):**

#### What Must Be Prefixed

- ✅ All functions
- ✅ All classes
- ✅ All hooks (actions and filters)
- ✅ Public variables and constants
- ✅ Database table names and options
- ✅ Custom post types and taxonomies
- ✅ Custom image sizes
- ✅ Script and style handles
- ✅ Shortcodes
- ✅ Widget classes
- ✅ REST API routes

#### Prefix Format Rules

```php
// ✅ CORRECT PREFIX FORMATS
themename_function_name()
authorname_function_name()
pluginname_function_name()

// ❌ INCORRECT PREFIX FORMATS
wp_function_name()      // Reserved for WordPress core
_function_name()        // Cannot start with underscore
-function_name()        // Cannot start with hyphen
```

#### Example Implementation

```php
// ✅ CORRECT
function sorobindu_ai_agent_init() {
    // Plugin initialization
}

add_action( 'init', 'sorobindu_ai_agent_init' );

class Sorobindu_AI_Agent_Admin {
    // Admin class
}

define( 'SOROBINDU_AI_AGENT_VERSION', '1.0.0' );

register_post_type( 'sorobindu_conversation', $args );

// ❌ INCORRECT - Will be rejected
function init_plugin() {
    // Generic function name
}

class Admin {
    // Generic class name
}
```

### Third-Party Scripts Exception

**Do NOT prefix third-party libraries** to avoid double-loading issues when multiple plugins use the same library.

---

## Documentation Requirements

### Mandatory Documentation

| Requirement | Details |
|-------------|---------|
| Language | English only |
| Format | PDF or HTML |
| Accessibility | Must be publicly accessible online |
| Coverage | Installation, customization, and usage |

### Documentation Must Include

1. **Installation Guide**
   - Server requirements
   - Step-by-step installation process
   - Activation instructions
   - Initial configuration

2. **Feature Documentation**
   - Complete feature list with descriptions
   - Screenshots/visuals for each feature
   - Use cases and examples

3. **Customization Guide**
   - Settings explanation
   - Hooks and filters available
   - Template customization (if applicable)

4. **Troubleshooting**
   - Common issues and solutions
   - FAQ section
   - Support contact information

### Documentation Standards

```markdown
✅ DO:
- Write for non-technical users
- Include visual guides and screenshots
- Provide step-by-step instructions
- Use clear, simple language
- Include a table of contents

❌ DON'T:
- Gate documentation behind purchase verification
- Use video-only documentation (supplement only)
- Assume coding knowledge
- Skip installation instructions
```

---

## Review Process

### Review Criteria

The Envato review team evaluates four primary areas:

1. **Item Presentation**
   - Visual aesthetics
   - Preview images quality
   - Professional appearance

2. **Item Information**
   - Metadata accuracy
   - Description quality
   - Tag relevance

3. **Technical Requirements**
   - Code quality
   - Security implementation
   - WordPress compatibility

4. **Legal Requirements**
   - Copyright compliance
   - Community standards
   - Content guidelines

### Review Outcomes

| Outcome | Description | Action Required |
|---------|-------------|-----------------|
| **Approved** | Item meets all standards | Published immediately |
| **Soft Rejection** | Minor issues need fixing | Address feedback, resubmit |
| **Hard Rejection** | Fundamental issues | Cannot resubmit same item |

### Soft Rejection Process

1. Access **Hidden Items** tab in Author Dashboard
2. Review all feedback points
3. Address **every single issue** mentioned
4. Click **Submit to update** after fixing

> ⚠️ **Important**: Partial fixes often result in re-rejection. Fix ALL noted issues before resubmitting.

### Hard Rejection Consequences

- Item cannot be resubmitted in current form
- Must create substantially different product
- **Attempting to resubmit may revoke upload rights**

### Common Hard Rejection Causes

- Quality below premium standards
- Legal or content guideline breaches
- Excessive similarity to existing marketplace items
- Duplicates freely available solutions
- Lack of commercial utility

---

## Security Compliance

### Core Security Principle

> **"Validate, sanitize, and escape everything"**
> - Validate and sanitize input immediately upon receipt
> - Escape output before rendering regardless of source

### Input Sanitization

**Always use WordPress sanitization functions:**

```php
// Text Fields
$clean_text = sanitize_text_field( $_POST['text_field'] );

// Email Addresses
$clean_email = sanitize_email( $_POST['email'] );

// File Names
$clean_filename = sanitize_file_name( $_POST['filename'] );

// Lowercase Alphanumeric Keys
$clean_key = sanitize_key( $_POST['key'] );

// Textarea Content
$clean_textarea = sanitize_textarea_field( $_POST['textarea'] );

// Title
$clean_title = sanitize_title( $_POST['title'] );

// URL
$clean_url = esc_url_raw( $_POST['url'] );

// HTML Content (allowed tags)
$clean_html = wp_kses_post( $_POST['html_content'] );
```

### Output Escaping

**Always escape output based on context:**

```php
// HTML Content
echo esc_html( $variable );

// HTML Attributes
echo '<input value="' . esc_attr( $variable ) . '">';

// URLs
echo '<a href="' . esc_url( $url ) . '">Link</a>';

// Textarea Content
echo '<textarea>' . esc_textarea( $content ) . '</textarea>';

// JavaScript
echo '<script>var data = ' . esc_js( $data ) . ';</script>';

// Translated Strings with Escaping
echo esc_html__( 'Text to translate', 'text-domain' );
echo esc_attr__( 'Attribute text', 'text-domain' );

// HTML with Specific Allowed Tags
echo wp_kses( $html, array(
    'a' => array(
        'href' => array(),
        'title' => array()
    ),
    'br' => array(),
    'em' => array(),
    'strong' => array(),
) );

// Post Content with Standard Tags
echo wp_kses_post( $post_content );
```

### Nonce Implementation

**Mandatory for all forms and AJAX requests:**

```php
// Creating Nonce for Forms
wp_nonce_field( 'sorobindu_save_settings', 'sorobindu_nonce' );

// Creating Nonce Programmatically
$nonce = wp_create_nonce( 'sorobindu_ajax_action' );

// Verifying Nonce in Form Processing
if ( ! isset( $_POST['sorobindu_nonce'] ) || 
     ! wp_verify_nonce( $_POST['sorobindu_nonce'], 'sorobindu_save_settings' ) ) {
    wp_die( 'Security check failed' );
}

// Verifying Nonce in Admin Pages
check_admin_referer( 'sorobindu_save_settings', 'sorobindu_nonce' );

// Verifying Nonce in AJAX
check_ajax_referer( 'sorobindu_ajax_action', 'nonce' );
```

### Capability Checking

**Always verify user permissions:**

```php
// Check Before Processing
if ( ! current_user_can( 'manage_options' ) ) {
    wp_die( 'Unauthorized access' );
}

// Check Specific Capabilities
if ( current_user_can( 'edit_posts' ) ) {
    // Allow action
}

// Check Against Specific Post
if ( current_user_can( 'edit_post', $post_id ) ) {
    // Allow editing
}
```

> ⚠️ **Critical**: Nonces verify intent, NOT identity. Always combine with capability checks.

---

## PHP Coding Standards

### Formatting Rules

| Rule | Standard |
|------|----------|
| Indentation | Tabs (not spaces) |
| Brace Style | Opening brace on same line |
| Line Length | Soft limit 100 characters |
| Blank Lines | One blank line between functions |

### Code Style Examples

```php
// ✅ CORRECT
function sorobindu_example_function( $param1, $param2 = '' ) {
    if ( empty( $param1 ) ) {
        return false;
    }

    foreach ( $items as $item ) {
        process_item( $item );
    }

    return true;
}

// ❌ INCORRECT
function sorobindu_example_function($param1, $param2 = '')
{
    if(empty($param1))
        return false;
    
    foreach($items as $item)
        process_item($item);
    
    return true;
}
```

### Equality Checks

```php
// ✅ CORRECT - Strict equality
if ( $value === true ) {
    // Do something
}

if ( $type === 'admin' ) {
    // Do something
}

// ❌ INCORRECT - Abstract equality
if ( $value == true ) {
    // Avoid this
}
```

### Prohibited PHP Practices

| Practice | Reason | Status |
|----------|--------|--------|
| `create_function()` | Deprecated in PHP 7.2 | ❌ Rejected |
| `eval()` | Security risk | ❌ Rejected |
| `@` error suppression | Hides errors | ❌ Rejected |
| PHP notices/warnings | Poor code quality | ❌ Rejected |
| Deprecated functions | Outdated code | ❌ Rejected |
| Short PHP tags `<?` | Compatibility issues | ❌ Rejected |

### Required Development Settings

```php
// wp-config.php during development
define( 'WP_DEBUG', true );
define( 'WP_DEBUG_LOG', true );
define( 'WP_DEBUG_DISPLAY', true );
define( 'SCRIPT_DEBUG', true );
```

---

## JavaScript Standards

### Formatting Rules

```javascript
// ✅ CORRECT
'use strict';

( function( $ ) {
    var sorobinduPlugin = {
        init: function() {
            this.bindEvents();
        },
        
        bindEvents: function() {
            $( document ).on( 'click', '.sorobindu-button', this.handleClick );
        },
        
        handleClick: function( event ) {
            event.preventDefault();
            // Handle click
        }
    };

    $( document ).ready( function() {
        sorobinduPlugin.init();
    } );

} )( jQuery );
```

### Required Practices

| Requirement | Details |
|-------------|---------|
| Strict Mode | `'use strict';` at beginning |
| Event Binding | Use `.on()` method only |
| Global Variables | Must be prefixed |
| Semicolons | Required for line termination |
| Console Errors | None allowed |

### Prohibited Practices

```javascript
// ❌ INCORRECT - Old event methods
$( '.button' ).click( function() {} );
$( '.element' ).bind( 'click', function() {} );
$( '.element' ).hover( function() {} );

// ✅ CORRECT - Use .on() method
$( document ).on( 'click', '.button', function() {} );
$( document ).on( 'mouseenter mouseleave', '.element', function() {} );
```

### Inline Scripts

```php
// ❌ INCORRECT - Inline scripts
echo '<script>var data = "value";</script>';

// ✅ CORRECT - Use wp_add_inline_script()
wp_add_inline_script( 'sorobindu-script', 'var sorobinduData = ' . wp_json_encode( $data ) . ';', 'before' );

// ✅ CORRECT - Use wp_localize_script()
wp_localize_script( 'sorobindu-script', 'sorobinduAjax', array(
    'ajaxurl' => admin_url( 'admin-ajax.php' ),
    'nonce'   => wp_create_nonce( 'sorobindu_nonce' ),
) );
```

---

## CSS Standards

### Formatting Rules

```css
/* ✅ CORRECT CSS Structure */

/**
 * Table of Contents
 *
 * 1.0 - Reset
 * 2.0 - Typography
 * 3.0 - Elements
 * 4.0 - Forms
 * 5.0 - Navigation
 * 6.0 - Content
 * 7.0 - Widgets
 * 8.0 - Media Queries
 */

/*--------------------------------------------------------------
1.0 Reset
--------------------------------------------------------------*/

.sorobindu-container {
    display: flex;
    flex-direction: column;
    padding: 20px;
    margin: 0 auto;
    max-width: 1200px;
}

.sorobindu-button {
    background-color: #0073aa;
    border: none;
    border-radius: 4px;
    color: #ffffff;
    cursor: pointer;
    padding: 10px 20px;
}

/*--------------------------------------------------------------
End Reset
--------------------------------------------------------------*/
```

### CSS Rules

| Rule | Requirement |
|------|-------------|
| Inline Styles | ❌ Prohibited |
| `!important` | Use sparingly, only when necessary |
| Selectors | Avoid excessive specificity |
| Comments | Section headers required |
| TOC | Table of contents at top |

### Loading CSS

```php
// ✅ CORRECT - Use wp_enqueue_style()
function sorobindu_enqueue_styles() {
    wp_enqueue_style(
        'sorobindu-public-css',
        plugin_dir_url( __FILE__ ) . 'css/sorobindu-public.css',
        array(),
        SOROBINDU_VERSION,
        'all'
    );
}
add_action( 'wp_enqueue_scripts', 'sorobindu_enqueue_styles' );

// ❌ INCORRECT - Direct loading
echo '<link rel="stylesheet" href="style.css">';
```

---

## Asset Loading Requirements

### Script Enqueuing

```php
/**
 * ✅ CORRECT Asset Loading
 */
function sorobindu_enqueue_scripts() {
    // Only load on specific pages
    if ( ! is_singular( 'product' ) ) {
        return;
    }

    wp_enqueue_script(
        'sorobindu-public-js',
        plugin_dir_url( __FILE__ ) . 'js/sorobindu-public.js',
        array( 'jquery' ),  // Dependencies
        SOROBINDU_VERSION,
        true  // Load in footer
    );

    // Pass data to script
    wp_localize_script( 'sorobindu-public-js', 'sorobinduData', array(
        'ajaxurl' => admin_url( 'admin-ajax.php' ),
        'nonce'   => wp_create_nonce( 'sorobindu_nonce' ),
        'i18n'    => array(
            'loading' => __( 'Loading...', 'sorobindu' ),
            'error'   => __( 'An error occurred', 'sorobindu' ),
        ),
    ) );
}
add_action( 'wp_enqueue_scripts', 'sorobindu_enqueue_scripts' );
```

### Critical Asset Rules

| Rule | Requirement |
|------|-------------|
| Loading Method | `wp_enqueue_script()` and `wp_enqueue_style()` ONLY |
| jQuery | ❌ **NEVER deregister default jQuery** |
| Core Scripts | ❌ Never load duplicates of core scripts |
| Conditional Loading | ✅ Load only where needed |
| Versioning | ✅ Include version numbers |

### Scripts Included in WordPress Core

**Do NOT include these libraries - use WordPress versions:**

- jQuery
- jQuery UI
- Underscore.js
- Backbone.js
- Moment.js
- Masonry
- Thickbox
- MediaElement.js

```php
// ✅ CORRECT - Use WordPress bundled scripts
wp_enqueue_script( 'jquery' );
wp_enqueue_script( 'jquery-ui-datepicker' );
wp_enqueue_script( 'underscore' );

// ❌ INCORRECT - Including your own versions
wp_enqueue_script( 'my-jquery', 'path/to/jquery.min.js' );
```

---

## Database Security

### Core Principle

> **Direct database queries are strongly discouraged.**
> Always use WordPress APIs when possible.

### Safe Database Methods

```php
global $wpdb;

// ✅ CORRECT - Using prepare() for all queries
$results = $wpdb->get_results(
    $wpdb->prepare(
        "SELECT * FROM {$wpdb->prefix}sorobindu_table WHERE user_id = %d AND status = %s",
        $user_id,
        $status
    )
);

// ✅ CORRECT - Using insert() method
$wpdb->insert(
    $wpdb->prefix . 'sorobindu_table',
    array(
        'user_id' => $user_id,
        'content' => $content,
        'created' => current_time( 'mysql' ),
    ),
    array( '%d', '%s', '%s' )
);

// ✅ CORRECT - Using update() method
$wpdb->update(
    $wpdb->prefix . 'sorobindu_table',
    array( 'status' => 'active' ),
    array( 'id' => $id ),
    array( '%s' ),
    array( '%d' )
);

// ✅ CORRECT - Using delete() method
$wpdb->delete(
    $wpdb->prefix . 'sorobindu_table',
    array( 'id' => $id ),
    array( '%d' )
);
```

### Prefer WordPress APIs Over Custom Tables

```php
// ✅ PREFERRED - Use Custom Post Types
register_post_type( 'sorobindu_item', $args );

// ✅ PREFERRED - Use Post Meta
update_post_meta( $post_id, '_sorobindu_data', $data );

// ✅ PREFERRED - Use Options API
update_option( 'sorobindu_settings', $settings );

// ✅ PREFERRED - Use Transients for Caching
set_transient( 'sorobindu_cache', $data, HOUR_IN_SECONDS );
```

### Prohibited Database Practices

```php
// ❌ NEVER DO THIS - SQL Injection vulnerable
$results = $wpdb->query( "SELECT * FROM table WHERE id = $_GET['id']" );

// ❌ NEVER DO THIS - Direct variable interpolation
$results = $wpdb->get_results( "SELECT * FROM table WHERE id = $id" );
```

---

## WordPress Compatibility

### Requirements

| Requirement | Details |
|-------------|---------|
| WordPress Version | Must work with latest WordPress |
| PHP Version | PHP 7.4+ recommended, 8.x compatible |
| WP_DEBUG | No errors with WP_DEBUG enabled |
| Deprecated Functions | None allowed |

### Plugin Header Requirements

```php
<?php
/**
 * Plugin Name:       SoroBindu AI Agent
 * Plugin URI:        https://sorobindu.com/plugins/ai-agent
 * Description:       AI-powered sales agent for WooCommerce stores.
 * Version:           1.0.0
 * Requires at least: 5.8
 * Requires PHP:      7.4
 * Author:            SoroBindu
 * Author URI:        https://sorobindu.com
 * License:           GPL v2 or later
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain:       sorobindu-ai-agent
 * Domain Path:       /languages
 * WC requires at least: 5.0
 * WC tested up to:   8.0
 */

// Prevent direct access
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}
```

### Version Compatibility Checking

```php
// Check WordPress Version
if ( version_compare( get_bloginfo( 'version' ), '5.8', '<' ) ) {
    add_action( 'admin_notices', 'sorobindu_wp_version_notice' );
    return;
}

// Check PHP Version
if ( version_compare( PHP_VERSION, '7.4', '<' ) ) {
    add_action( 'admin_notices', 'sorobindu_php_version_notice' );
    return;
}

// Check WooCommerce Dependency
if ( ! class_exists( 'WooCommerce' ) ) {
    add_action( 'admin_notices', 'sorobindu_wc_missing_notice' );
    return;
}
```

---

## Presentation & Image Requirements

### Cover Image (Main Thumbnail)

| Specification | Requirement |
|---------------|-------------|
| Recommended Size | 2340 × 1560 pixels |
| Minimum Size | 1170 × 780 pixels |
| Aspect Ratio | 3:2 (mandatory) |
| Max File Size | 20MB |
| Formats | JPEG, PNG, SVG, GIF |

### Thumbnail (Small Icon)

| Specification | Requirement |
|---------------|-------------|
| Size | 80 × 80 pixels (exact) |
| Format | JPEG, PNG |

### Inline Preview Image (CodeCanyon Specific)

| Specification | Requirement |
|---------------|-------------|
| Size | 590 × 300 pixels (exact) |
| Format | JPEG |

### Screenshot Gallery

| Specification | Requirement |
|---------------|-------------|
| Minimum Width | 570 pixels |
| Recommended Ratio | 3:2 |
| Maximum Images | 15 |
| Recommended Minimum | 3 images |

### Image Quality Guidelines

| Do ✅ | Don't ❌ |
|-------|---------|
| Use high-resolution source images | Upscale smaller images |
| Light/neutral backgrounds | Dark, cluttered backgrounds |
| Clean, professional design | Over-compressed images |
| Show actual plugin functionality | Excessive text/branding |
| Professional mockups | Misleading screenshots |

---

## Item Description & Metadata

### Title Requirements

| Rule | Requirement |
|------|-------------|
| Maximum Length | 100 characters |
| Characters | English only |
| Format | Title Case |
| Content | Descriptive, no keyword stuffing |

### Description Best Practices

```html
<!-- ✅ GOOD Description Structure -->
<h2>Plugin Name - Short Tagline</h2>

<p>Brief introduction explaining what the plugin does and who it's for.</p>

<h3>Key Features</h3>
<ul>
    <li>Feature 1 with brief explanation</li>
    <li>Feature 2 with brief explanation</li>
    <li>Feature 3 with brief explanation</li>
</ul>

<h3>Requirements</h3>
<ul>
    <li>WordPress 5.8+</li>
    <li>PHP 7.4+</li>
    <li>WooCommerce 5.0+ (if applicable)</li>
</ul>

<h3>Documentation</h3>
<p>Link to documentation</p>

<h3>Support</h3>
<p>Support policy and contact information</p>

<h3>Changelog</h3>
<p>Version history</p>
```

### Required Disclosures

| Item | Requirement |
|------|-------------|
| Assets Not Included | List all preview assets not in download |
| Fonts Used | Credit with names and links |
| PhotoDune Images | Proper attribution |
| Third-Party Libraries | List all included |
| External Services | Disclose API connections |

### Tags

| Rule | Requirement |
|------|-------------|
| Maximum | 15 tags |
| Format | Can include phrases |
| Content | Accurate to functionality |
| Prohibited | Competitor names, keyword stuffing |

---

## Licensing Structure

### Regular License

| Aspect | Details |
|--------|---------|
| Price | Base price (e.g., $39) |
| Usage | End products distributed free |
| Copies | Unlimited for free distribution |
| End Users | Cannot charge end users |

### Extended License

| Aspect | Details |
|--------|---------|
| Price | 5-50× Regular License (e.g., $2,800) |
| Usage | Products sold to customers |
| Copies | Unlimited for paid distribution |
| End Users | Can charge end users |

### License Selection Guide

```
Regular License:
├── Personal websites
├── Free WordPress themes
├── Free web applications
├── Client projects (single end product)
└── Internal company use

Extended License:
├── Themes/plugins for sale
├── SaaS applications
├── Paid web applications
└── Products with recurring fees
```

---

## Revenue Sharing & Earnings

### Exclusive Authors

| Total Sales | Author Rate | Envato Fee |
|-------------|-------------|------------|
| Starting | 50% | 50% |
| $3,750+ | 51.25% | 48.75% |
| $7,500+ | 52.5% | 47.5% |
| ... | +1.25% per $3,750 | ... |
| Maximum | 70% | 30% |

### Non-Exclusive Authors

| Rate Type | Author Rate | Envato Fee |
|-----------|-------------|------------|
| Fixed Rate | 36% | 55% |

### Payment Schedule

| Event | Timing |
|-------|--------|
| Earnings Consolidation | 8th of each month |
| Payout Processing | 15th of each month |
| Minimum Withdrawal | $50 USD |

### Payment Methods

- PayPal
- Bank Transfer
- Payoneer
- Wise
- Revolut

### Tax Considerations

| Documentation | Withholding |
|---------------|-------------|
| No W8 Form | 28% withheld |
| With W8 + Tax ID | Varies by treaty |

---

## Exclusivity Policy

### Exclusive Authors

| Benefits | Restrictions |
|----------|-------------|
| Higher earnings (up to 70%) | Cannot sell elsewhere |
| Progressive fee reduction | No personal website sales |
| Promotional priority | No giveaways |
| Earlier Elite status access | Full commitment to Envato |

### Non-Exclusive Authors

| Benefits | Restrictions |
|----------|-------------|
| Sell anywhere | Fixed 36% rate |
| Multiple platforms | No fee reduction |
| Full flexibility | Lower promotional priority |

### Managing Both

You can maintain two separate accounts:
- One exclusive account
- One non-exclusive account
- Different items on each

---

## Privacy & Legal Compliance

### Data Handling

| Requirement | Details |
|-------------|---------|
| GDPR Awareness | Handle data per applicable law |
| Data Collection | Disclose in item description |
| Third-Party Services | Document integrations |
| Tracking/Cookies | Note usage in documentation |

### EU Digital Services Act

| Requirement | Details |
|-------------|---------|
| Trader Status | Verify if EU-based |
| Contact Information | Display if trader |
| Compliance | Follow DSA requirements |

### Privacy Best Practices

```php
// ✅ GOOD - Privacy-conscious implementation

// 1. Only collect necessary data
function sorobindu_save_user_data( $user_id ) {
    // Only save essential data
    update_user_meta( $user_id, '_sorobindu_preferences', $preferences );
}

// 2. Provide data export
function sorobindu_export_user_data( $user_id ) {
    return array(
        'preferences' => get_user_meta( $user_id, '_sorobindu_preferences', true ),
        // Include all stored data
    );
}

// 3. Provide data deletion
function sorobindu_delete_user_data( $user_id ) {
    delete_user_meta( $user_id, '_sorobindu_preferences' );
    // Delete all user data
}

// 4. Hook into WordPress privacy tools
add_filter( 'wp_privacy_personal_data_exporters', 'sorobindu_register_exporter' );
add_filter( 'wp_privacy_personal_data_erasers', 'sorobindu_register_eraser' );
```

---

## Prohibited Content

### Absolutely Forbidden

| Category | Description |
|----------|-------------|
| Adult Content | Sexually explicit material |
| Child Safety | Any child exploitation content |
| Hate Speech | Content targeting protected groups |
| Violence | Incitement or graphic violence |
| Fraud | Misleading or deceptive content |
| Illegal Activities | Content facilitating crimes |
| Malware | Security threats, malicious code |
| Copyright Violation | Unauthorized copyrighted content |
| AI Training | Content for training AI models |

### Content Restrictions

- No unauthorized tracking
- No data collection without disclosure
- No cryptocurrency/NFT primary focus
- No regulated goods promotion
- No pharmaceutical content

> ⚠️ **Warning**: Uploading prohibited content may result in immediate account termination.

---

## Common Rejection Reasons

### Technical Rejections

| Issue | Solution |
|-------|----------|
| Missing unique prefix | Add prefix to ALL functions, classes, hooks |
| Improper output escaping | Use `esc_*()` functions everywhere |
| Missing nonce verification | Add nonces to all forms and AJAX |
| Direct database queries | Use `$wpdb->prepare()` or WordPress APIs |
| Deregistering jQuery | Never modify core scripts |
| PHP errors/warnings | Test with WP_DEBUG enabled |

### Quality Rejections

| Issue | Solution |
|-------|----------|
| Insufficient documentation | Create comprehensive user guide |
| Poor code organization | Follow file structure standards |
| Lack of unique value | Differentiate from free alternatives |
| Inadequate presentation | Professional images and descriptions |

### Presentation Rejections

| Issue | Solution |
|-------|----------|
| Wrong image sizes | Follow exact specifications |
| Missing demo | Provide live preview |
| Incomplete description | Detail all features and requirements |
| Poor image quality | Use high-resolution sources |

---

## Pre-Submission Checklist

### Code Quality

- [ ] All functions/classes use unique prefix
- [ ] No PHP errors with WP_DEBUG enabled
- [ ] All output properly escaped
- [ ] All input sanitized
- [ ] Nonces implemented for forms/AJAX
- [ ] Capability checks in place
- [ ] No deprecated functions
- [ ] No `eval()` or `create_function()`
- [ ] Database queries use `$wpdb->prepare()`
- [ ] Assets loaded via `wp_enqueue_*()`
- [ ] Default jQuery not modified
- [ ] Strict equality checks used

### File Organization

- [ ] No files in root directory
- [ ] Logical folder hierarchy
- [ ] Proper file naming (lowercase, hyphens)
- [ ] No empty folders
- [ ] No unused files
- [ ] Third-party libraries not prefixed

### Documentation

- [ ] English PDF or HTML documentation
- [ ] Publicly accessible online
- [ ] Installation instructions
- [ ] Feature explanations
- [ ] Customization guide
- [ ] Troubleshooting section
- [ ] Written for non-technical users

### Presentation

- [ ] Cover image: 2340×1560 (or 1170×780 min)
- [ ] Thumbnail: 80×80 exact
- [ ] Inline preview: 590×300 JPEG
- [ ] 3+ preview screenshots
- [ ] Live demo available
- [ ] Professional quality images
- [ ] Accurate description
- [ ] All assets credited

### Legal

- [ ] No copyrighted content
- [ ] All third-party licenses valid
- [ ] Proper attributions included
- [ ] Privacy disclosures if collecting data
- [ ] Terms compliance verified

---

## Useful Resources

### Official Envato Documentation

- [WordPress Plugin Requirements](https://help.author.envato.com/hc/en-us/articles/360000510603-WordPress-Plugin-Requirements)
- [Code Item Preparation](https://help.author.envato.com/hc/en-us/articles/360000471583-Code-Item-Preparation-Technical-Requirements)
- [Common Rejection Factors](https://help.author.envato.com/hc/en-us/articles/360000536823-Common-Rejection-Factors-for-Code-Items)
- [Item Presentation Requirements](https://help.author.envato.com/hc/en-us/articles/360000424863-Item-Presentation-Requirements)
- [Exclusivity Policy](https://help.author.envato.com/hc/en-us/articles/360000471226-Exclusivity-Policy)

### WordPress Coding Standards

- [WordPress Coding Standards](https://developer.wordpress.org/coding-standards/)
- [Plugin Handbook](https://developer.wordpress.org/plugins/)
- [Theme Security](https://developer.wordpress.org/themes/theme-security/)

### Tools

- [WPCS for Envato](https://github.com/wpsh/wpcs-for-envato) - Coding standards validation
- [Plugin Check (PCP)](https://wordpress.org/plugins/plugin-check/) - WordPress plugin checker
- [Query Monitor](https://wordpress.org/plugins/query-monitor/) - Development debugging

### Community Resources

- [Envato Forums](https://forums.envato.com/)
- [Envato Discord](https://discord.gg/envato)
- [Review Queue Status](https://quality.market.envato.com/codecanyon)

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | December 2025 | Initial comprehensive guide |

---

> **Document prepared for NexaLance WordPress Plugin Development**
> 
> Reference this guide for all CodeCanyon plugin submissions to ensure first-time approval success.

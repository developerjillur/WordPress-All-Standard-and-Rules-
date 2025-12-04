# WordPress.org Plugin Submission: Complete Standards & Guidelines

> **Last Updated:** December 2024  
> **Review Queue Status:** ~7-9 weeks (improved from 37 weeks)  
> **Mandatory Requirement:** Plugin Check (PCP) automated scanning since September 2024

---

## Table of Contents

1. [Overview & Current Statistics](#1-overview--current-statistics)
2. [File Structure Requirements](#2-file-structure-requirements)
3. [Plugin Header Requirements](#3-plugin-header-requirements)
4. [Readme.txt Specification](#4-readmetxt-specification)
5. [Plugin Naming Rules](#5-plugin-naming-rules)
6. [The Review Process](#6-the-review-process)
7. [Security Compliance](#7-security-compliance)
8. [Privacy & GDPR Compliance](#8-privacy--gdpr-compliance)
9. [Licensing Requirements (GPL)](#9-licensing-requirements-gpl)
10. [Code Quality Standards](#10-code-quality-standards)
11. [Internationalization (i18n)](#11-internationalization-i18n)
12. [Accessibility Standards](#12-accessibility-standards)
13. [Prohibited Practices](#13-prohibited-practices)
14. [Commercial & Freemium Rules](#14-commercial--freemium-rules)
15. [External Services & API Rules](#15-external-services--api-rules)
16. [Block Plugins (Block Directory)](#16-block-plugins-block-directory)
17. [Common Rejection Reasons](#17-common-rejection-reasons)
18. [Pre-Submission Checklist](#18-pre-submission-checklist)
19. [Tools & Resources](#19-tools--resources)
20. [Code Examples & Templates](#20-code-examples--templates)

---

## 1. Overview & Current Statistics

### Current State (2024-2025)

| Metric | Value |
|--------|-------|
| Total Hosted Plugins | ~100,000 |
| Average Review Cycles to Approval | 6.19 |
| Developer Success Rate | 64.2% |
| First Reviews Using Automation | 85.3% |
| Current Wait Time | ~7-9 weeks |
| Response Deadline After Feedback | 10 business days |
| Auto-Rejection After Inactivity | 3 months |

### Key Changes in 2024

- **Plugin Check (PCP) is now mandatory** - Submissions failing automated checks are blocked before human review
- **Two-Factor Authentication required** for all plugin submitters (October 2024)
- **Automatic security scans** now run on all plugin updates, not just initial submissions
- **AI-assisted reviews** help automate 85%+ of first-pass reviews

---

## 2. File Structure Requirements

### SVN Repository Structure

```
/assets/
    banner-772x250.png          # Plugin banner (required for visibility)
    banner-1544x500.png         # High-DPI banner (optional)
    icon-128x128.png            # Plugin icon
    icon-256x256.png            # High-DPI icon
    screenshot-1.png            # Screenshots (numbered sequentially)
    screenshot-2.png
    
/tags/
    /1.0.0/                     # Version folders
        plugin-name.php
        readme.txt
        /includes/
        /admin/
        /public/
    /1.0.1/
    /1.1.0/
    
/trunk/                         # Latest development code
    plugin-name.php             # Main plugin file (MUST be in root)
    readme.txt
    uninstall.php               # Clean uninstall handler
    /includes/
    /admin/
    /public/
    /languages/
```

### Critical File Placement Rules

| Rule | Correct | Incorrect |
|------|---------|-----------|
| Main plugin file location | `/trunk/my-plugin.php` | `/trunk/my-plugin/my-plugin.php` |
| Assets location | `/assets/` (root level) | `/trunk/assets/` |
| Version tags | `/tags/1.0.0/` | `/tags/v1.0.0/` or `/tags/latest/` |

### File Naming Conventions

```
✅ Correct:
- my-awesome-plugin.php
- class-my-plugin-admin.php
- my-plugin-functions.php

❌ Incorrect:
- MyAwesomePlugin.php
- my_awesome_plugin.php
- plugin.php (too generic)
```

### Files to EXCLUDE from Submission

```
# Development files - MUST be removed
/node_modules/
/vendor/                    # Unless dependencies are required
/tests/
/test/
/.git/
/.svn/
/.github/
/bin/
/.editorconfig
/.gitignore
/.gitattributes
/phpunit.xml
/phpcs.xml
/composer.lock
/package-lock.json
/Gruntfile.js
/gulpfile.js
/webpack.config.js
/*.map                      # Source maps
```

---

## 3. Plugin Header Requirements

### Mandatory Header Format

The header must appear within the **first 8KB (8,192 bytes)** of the main plugin file:

```php
<?php
/**
 * Plugin Name:       My Awesome Plugin
 * Plugin URI:        https://example.com/my-awesome-plugin
 * Description:       A brief description of what the plugin does. Max 140 characters recommended.
 * Version:           1.0.0
 * Requires at least: 6.0
 * Requires PHP:      7.4
 * Author:            Your Name
 * Author URI:        https://example.com
 * License:           GPL v2 or later
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain:       my-awesome-plugin
 * Domain Path:       /languages
 * Network:           true
 * Update URI:        https://example.com/my-plugin-updates
 *
 * @package MyAwesomePlugin
 */
```

### Header Fields Reference

| Field | Required | Max Length | Notes |
|-------|----------|------------|-------|
| Plugin Name | ✅ Yes | 150 chars | Must be unique, no trademarks |
| Description | Recommended | 140 chars | Shows in plugin list |
| Version | ✅ Yes | - | Semantic versioning (X.Y.Z) |
| Requires at least | Recommended | - | Minimum WordPress version |
| Requires PHP | Recommended | - | Minimum PHP version |
| Author | Recommended | - | Your name or company |
| License | ✅ Yes | - | Must be GPL compatible |
| Text Domain | ✅ Yes | - | Must match plugin slug exactly |
| Domain Path | If using translations | - | Relative path to languages folder |
| Network | Optional | - | Set `true` for multisite-only |
| Update URI | Optional | - | For self-hosted updates (not WordPress.org) |

### Version Numbering Standards

```
Format: MAJOR.MINOR.PATCH

Examples:
1.0.0   - Initial release
1.0.1   - Bug fix release
1.1.0   - New feature added
2.0.0   - Major changes, possible breaking changes

❌ Invalid formats:
- 1.0
- v1.0.0
- 1.0.0-beta
- 1.0.0.1
```

---

## 4. Readme.txt Specification

### Complete Readme.txt Template

```
=== My Awesome Plugin ===
Contributors: yourusername, anotherusername
Donate link: https://example.com/donate
Tags: tag1, tag2, tag3, tag4, tag5
Requires at least: 6.0
Tested up to: 6.4
Requires PHP: 7.4
Stable tag: 1.0.0
License: GPLv2 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html

Short description of the plugin. Must be 150 characters or fewer.

== Description ==

This is the long description. No limit, but be concise and informative.

**Features:**

* Feature one
* Feature two
* Feature three

**Links:**

* [Documentation](https://example.com/docs)
* [Support Forum](https://wordpress.org/support/plugin/my-awesome-plugin)
* [GitHub Repository](https://github.com/username/my-awesome-plugin)

== Installation ==

1. Upload the plugin files to `/wp-content/plugins/my-awesome-plugin`, or install through the WordPress plugins screen.
2. Activate the plugin through the 'Plugins' screen in WordPress.
3. Use the Settings -> My Plugin screen to configure the plugin.

= Minimum Requirements =

* WordPress 6.0 or greater
* PHP version 7.4 or greater

== Frequently Asked Questions ==

= How do I configure the plugin? =

Navigate to Settings -> My Plugin to access the configuration options.

= Is this plugin compatible with WooCommerce? =

Yes, the plugin is fully compatible with WooCommerce 8.0 and above.

== Screenshots ==

1. This is the first screenshot description. Screenshots are in /assets/.
2. This is the second screenshot description.
3. Admin settings page.

== Changelog ==

= 1.0.0 =
* Initial release

= 0.9.0 =
* Beta release for testing

== Upgrade Notice ==

= 1.0.0 =
Initial stable release. Recommended for all users.

== External Services ==

This plugin connects to the following external services:

**Service Name API**
* Purpose: Describe why the plugin connects to this service
* Data transmitted: List what data is sent
* When transmitted: Describe when the connection occurs
* Service URL: https://api.service.com
* Privacy Policy: https://service.com/privacy
* Terms of Service: https://service.com/terms

== Privacy Policy ==

This plugin stores the following data:
* List any personal data collected
* Explain data retention periods
* Describe how data is used
```

### Readme.txt Field Requirements

| Field | Required | Notes |
|-------|----------|-------|
| Plugin Name (title) | ✅ Yes | In `=== Name ===` format |
| Contributors | ✅ Yes | WordPress.org usernames only |
| Tags | ✅ Yes | 1-5 tags, comma-separated |
| Requires at least | ✅ Yes | WordPress version |
| Tested up to | ✅ Yes | Latest tested WordPress version |
| Stable tag | ✅ Yes | Must match a `/tags/` folder |
| License | ✅ Yes | GPL-compatible license |
| Short Description | ✅ Yes | Max 150 characters |
| Description | ✅ Yes | Detailed description |
| Installation | ✅ Yes | Step-by-step instructions |
| FAQ | Recommended | Common questions |
| Screenshots | Recommended | Numbered to match files |
| Changelog | ✅ Yes | Version history |
| Upgrade Notice | Recommended | Per-version upgrade notes |
| External Services | If applicable | **Required if connecting externally** |

### Stable Tag Rules

```
✅ Correct:
Stable tag: 1.0.0    # Points to /tags/1.0.0/

❌ Incorrect:
Stable tag: trunk    # Deprecated, causes issues
Stable tag: 1.0      # Must match full version
Stable tag: latest   # Invalid
```

### Readme Validation

Always validate before submission:
```
https://wordpress.org/plugins/developers/readme-validator/
```

---

## 5. Plugin Naming Rules

### Naming Restrictions

| Rule | Example |
|------|---------|
| No WordPress trademark | ❌ "WordPress SEO Master" |
| No WP as first term | ❌ "WP Contact Form" |
| No Woo trademark | ❌ "Woo Product Manager" |
| No third-party trademarks | ❌ "Elementor Addon Pack" |
| Must be descriptive | ❌ "Plugin" or "Tool" |
| No version numbers | ❌ "Contact Form 2.0" |

### Correct Naming Patterns

```
✅ Correct Format:
"Contact Form for Elementor"           (describes what it does + integration)
"CSV Exporter for Gravity Forms"       (function + platform)
"Simple SEO Tools"                     (descriptive, no trademarks)
"Advanced Custom Fields Exporter"      (if you have permission)

❌ Incorrect Format:
"Elementor Contact Form"               (trademark first)
"WP Super Cache Pro"                   (WP prefix + misleading "Pro")
"WordPress Ultimate SEO"               (WordPress trademark)
"Gravity Forms CSV"                    (trademark first)
```

### Slug Generation Rules

The slug is auto-generated and **cannot be changed after approval**:

```
Plugin Name: "My Awesome Contact Form"
Generated Slug: my-awesome-contact-form

Rules:
- Lowercase conversion
- Spaces → hyphens
- Special characters removed
- Numbers allowed
- Max ~200 characters (practical limit)
```

---

## 6. The Review Process

### Submission Workflow

```
┌─────────────────────────────────────────────────────────────────┐
│  1. PREPARATION                                                  │
│     ├── Run Plugin Check locally                                │
│     ├── Validate readme.txt                                     │
│     ├── Enable 2FA on WordPress.org account                     │
│     └── Create ZIP file (<10MB, no dev files)                   │
└─────────────────────────────────────────────────────────────────┘
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  2. SUBMISSION                                                   │
│     ├── Submit at wordpress.org/plugins/developers/add/         │
│     ├── Receive confirmation email with assigned slug           │
│     └── Plugin enters review queue                              │
└─────────────────────────────────────────────────────────────────┘
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  3. AUTOMATED REVIEW (Plugin Check)                             │
│     ├── Security category checks                                │
│     ├── Performance checks                                      │
│     ├── Plugin Repo category checks                             │
│     └── ❌ Fails = Blocked before human review                  │
└─────────────────────────────────────────────────────────────────┘
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  4. MANUAL REVIEW                                                │
│     ├── Same reviewer throughout process                        │
│     ├── Security implementation review                          │
│     ├── Code quality assessment                                 │
│     ├── Guideline compliance check                              │
│     └── Documentation review                                    │
└─────────────────────────────────────────────────────────────────┘
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  5. FEEDBACK LOOP                                                │
│     ├── Receive feedback via email                              │
│     ├── Reply to SAME email thread (don't create new)           │
│     ├── Respond within 10 business days                         │
│     ├── Average: 6.19 cycles to approval                        │
│     └── Auto-rejected after 3 months inactivity                 │
└─────────────────────────────────────────────────────────────────┘
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  6. APPROVAL                                                     │
│     ├── Receive SVN credentials                                 │
│     ├── Upload plugin to SVN repository                         │
│     ├── Plugin goes live on directory                           │
│     └── Future updates: commit to SVN (auto-reviewed)           │
└─────────────────────────────────────────────────────────────────┘
```

### Timeline Reference

| Stage | Target | Warning | Critical |
|-------|--------|---------|----------|
| Initial Review | 7 days | 7-14 days | >14 days |
| Response to Feedback | 10 business days | - | Auto-close at 3 months |
| Total Process | ~7-9 weeks | Variable | - |

### Communication Guidelines

```
✅ DO:
- Reply to existing email threads only
- Be professional and patient
- Provide clear explanations of changes made
- Ask specific questions if unclear
- Wait 7 business days before follow-up

❌ DON'T:
- Send new emails to plugins@wordpress.org
- Resubmit the plugin while in review
- Contact individual reviewers directly
- Submit multiple plugins simultaneously (unless >1M installs)
- Be confrontational or impatient
```

### Concurrent Submission Limits

| Active Installs | Simultaneous Submissions |
|-----------------|--------------------------|
| < 1,000,000 | 1 plugin |
| ≥ 1,000,000 | Up to 10 plugins |

---

## 7. Security Compliance

### 7.1 Nonce Verification (CSRF Protection)

Nonces prevent Cross-Site Request Forgery attacks.

#### Creating Nonces

```php
// For forms
wp_nonce_field( 'my_plugin_action', 'my_plugin_nonce' );

// For URLs
$url = wp_nonce_url( admin_url( 'admin.php?page=my-plugin' ), 'my_action', 'my_nonce' );

// For AJAX
wp_create_nonce( 'my_ajax_action' );
```

#### Verifying Nonces

```php
// Form verification
if ( ! isset( $_POST['my_plugin_nonce'] ) || 
     ! wp_verify_nonce( $_POST['my_plugin_nonce'], 'my_plugin_action' ) ) {
    wp_die( __( 'Security check failed.', 'my-plugin' ) );
}

// Admin page verification
check_admin_referer( 'my_plugin_action', 'my_plugin_nonce' );

// AJAX verification
check_ajax_referer( 'my_ajax_action', 'security' );

// Manual verification with wp_verify_nonce
if ( ! wp_verify_nonce( $_REQUEST['_wpnonce'], 'my_action' ) ) {
    wp_die( 'Invalid nonce' );
}
```

#### Nonce Lifetime

```
Default: 24 hours
Actual validity: 12-24 hours (due to tick system)

⚠️ IMPORTANT: Nonces verify intent, NOT identity
   Always combine with capability checks!
```

### 7.2 Capability Checks

Always verify user permissions before privileged operations.

```php
// Check specific capability
if ( ! current_user_can( 'manage_options' ) ) {
    wp_die( __( 'You do not have permission to access this page.', 'my-plugin' ) );
}

// Check post-specific capability
if ( ! current_user_can( 'edit_post', $post_id ) ) {
    wp_die( __( 'You cannot edit this post.', 'my-plugin' ) );
}

// Common capabilities
'manage_options'      // Administrators
'edit_posts'          // Authors and above
'publish_posts'       // Authors and above
'edit_others_posts'   // Editors and above
'delete_posts'        // Authors and above
'upload_files'        // Authors and above
'edit_users'          // Administrators
'install_plugins'     // Super Admins (multisite)
```

#### Common Mistake: is_admin() vs current_user_can()

```php
// ❌ WRONG - is_admin() only checks if on admin page, NOT permissions
if ( is_admin() ) {
    // Dangerous - any logged-in user can access admin pages
    delete_option( 'important_data' );
}

// ✅ CORRECT - Verify actual capability
if ( current_user_can( 'manage_options' ) ) {
    delete_option( 'important_data' );
}
```

### 7.3 Complete Security Pattern

```php
/**
 * Process form submission with full security
 */
function my_plugin_process_form() {
    // 1. Verify nonce FIRST
    if ( ! isset( $_POST['my_plugin_nonce'] ) || 
         ! wp_verify_nonce( sanitize_text_field( wp_unslash( $_POST['my_plugin_nonce'] ) ), 'my_plugin_save' ) ) {
        wp_die( esc_html__( 'Security verification failed.', 'my-plugin' ) );
    }
    
    // 2. Check capability SECOND
    if ( ! current_user_can( 'manage_options' ) ) {
        wp_die( esc_html__( 'You do not have permission to perform this action.', 'my-plugin' ) );
    }
    
    // 3. Sanitize ALL input
    $title = isset( $_POST['title'] ) ? sanitize_text_field( wp_unslash( $_POST['title'] ) ) : '';
    $email = isset( $_POST['email'] ) ? sanitize_email( wp_unslash( $_POST['email'] ) ) : '';
    $url = isset( $_POST['url'] ) ? esc_url_raw( wp_unslash( $_POST['url'] ) ) : '';
    $content = isset( $_POST['content'] ) ? wp_kses_post( wp_unslash( $_POST['content'] ) ) : '';
    $number = isset( $_POST['count'] ) ? absint( $_POST['count'] ) : 0;
    
    // 4. Validate data
    if ( empty( $title ) ) {
        wp_die( esc_html__( 'Title is required.', 'my-plugin' ) );
    }
    
    if ( ! is_email( $email ) ) {
        wp_die( esc_html__( 'Invalid email address.', 'my-plugin' ) );
    }
    
    // 5. Process data safely
    update_option( 'my_plugin_title', $title );
    update_option( 'my_plugin_email', $email );
    
    // 6. Redirect to prevent resubmission
    wp_safe_redirect( add_query_arg( 'updated', 'true', wp_get_referer() ) );
    exit;
}
add_action( 'admin_post_my_plugin_save', 'my_plugin_process_form' );
```

### 7.4 Input Sanitization Functions

| Function | Use Case | Example |
|----------|----------|---------|
| `sanitize_text_field()` | Single-line text | Names, titles |
| `sanitize_textarea_field()` | Multi-line text | Descriptions |
| `sanitize_email()` | Email addresses | user@example.com |
| `sanitize_url()` | URLs (for display) | Links |
| `esc_url_raw()` | URLs (for database) | Storing URLs |
| `sanitize_file_name()` | File names | Uploads |
| `sanitize_title()` | Slugs | Post slugs |
| `sanitize_key()` | Lowercase alphanumeric | Option keys |
| `absint()` | Positive integers | IDs, counts |
| `intval()` | Any integer | Numbers (can be negative) |
| `floatval()` | Decimal numbers | Prices |
| `wp_kses()` | HTML with allowed tags | Custom HTML |
| `wp_kses_post()` | HTML (post content allowed tags) | Rich content |
| `sanitize_hex_color()` | Hex colors | #ffffff |

### 7.5 Output Escaping Functions

**Rule: Escape at the point of output, not before storage**

| Function | Context | Example |
|----------|---------|---------|
| `esc_html()` | HTML content | `<p><?php echo esc_html( $text ); ?></p>` |
| `esc_attr()` | HTML attributes | `<input value="<?php echo esc_attr( $value ); ?>">` |
| `esc_url()` | URLs (href, src) | `<a href="<?php echo esc_url( $link ); ?>">` |
| `esc_js()` | Inline JavaScript | `onclick="alert('<?php echo esc_js( $msg ); ?>');"` |
| `esc_textarea()` | Textarea content | `<textarea><?php echo esc_textarea( $text ); ?></textarea>` |
| `wp_kses()` | Allow specific HTML | Content with safe tags |
| `wp_kses_post()` | Post-like content | User-submitted HTML |

#### Combined Escape + Translate Functions

```php
// Escape and translate
esc_html__( 'Text to translate', 'my-plugin' );     // Returns escaped string
esc_html_e( 'Text to translate', 'my-plugin' );     // Echoes escaped string
esc_attr__( 'Attribute text', 'my-plugin' );        // Returns for attributes
esc_attr_e( 'Attribute text', 'my-plugin' );        // Echoes for attributes

// Example usage
<h1><?php esc_html_e( 'Settings', 'my-plugin' ); ?></h1>
<input placeholder="<?php esc_attr_e( 'Enter name', 'my-plugin' ); ?>">
```

### 7.6 Database Security

#### Always Use $wpdb->prepare()

```php
global $wpdb;

// ✅ CORRECT - Using prepare with placeholders
$results = $wpdb->get_results(
    $wpdb->prepare(
        "SELECT * FROM {$wpdb->prefix}my_table WHERE user_id = %d AND status = %s",
        $user_id,
        $status
    )
);

// Placeholders:
// %d - Integer
// %s - String
// %f - Float
// %i - Identifier (WordPress 6.2+)

// ❌ WRONG - Direct variable interpolation
$results = $wpdb->get_results(
    "SELECT * FROM {$wpdb->prefix}my_table WHERE user_id = $user_id"
);

// ❌ WRONG - esc_sql alone (doesn't add quotes)
$results = $wpdb->get_results(
    "SELECT * FROM {$wpdb->prefix}my_table WHERE name = " . esc_sql( $name )
);
```

#### Safe Helper Methods

```php
// Insert - automatically escapes
$wpdb->insert(
    $wpdb->prefix . 'my_table',
    array(
        'user_id' => $user_id,
        'name'    => $name,
        'email'   => $email,
    ),
    array( '%d', '%s', '%s' )  // Format specifiers
);

// Update - automatically escapes
$wpdb->update(
    $wpdb->prefix . 'my_table',
    array( 'name' => $new_name ),           // Data
    array( 'id' => $id ),                   // Where
    array( '%s' ),                          // Data format
    array( '%d' )                           // Where format
);

// Delete - automatically escapes
$wpdb->delete(
    $wpdb->prefix . 'my_table',
    array( 'id' => $id ),
    array( '%d' )
);
```

### 7.7 File Security

#### Prevent Direct Access

Add to the top of EVERY PHP file:

```php
<?php
// Prevent direct access
if ( ! defined( 'ABSPATH' ) ) {
    exit; // Exit if accessed directly
}

// Alternative methods (all acceptable):
defined( 'ABSPATH' ) || exit;
defined( 'ABSPATH' ) or die( 'No direct access!' );
if ( ! defined( 'WPINC' ) ) { die; }
```

#### Safe File Uploads

```php
function my_plugin_handle_upload( $file ) {
    // Check for upload errors
    if ( $file['error'] !== UPLOAD_ERR_OK ) {
        return new WP_Error( 'upload_error', __( 'Upload failed.', 'my-plugin' ) );
    }
    
    // Validate file type
    $allowed_types = array( 'jpg', 'jpeg', 'png', 'gif', 'pdf' );
    $file_info = wp_check_filetype( $file['name'] );
    
    if ( ! in_array( $file_info['ext'], $allowed_types, true ) ) {
        return new WP_Error( 'invalid_type', __( 'File type not allowed.', 'my-plugin' ) );
    }
    
    // Sanitize filename
    $filename = sanitize_file_name( $file['name'] );
    
    // Use WordPress upload handling
    require_once ABSPATH . 'wp-admin/includes/file.php';
    
    $upload = wp_handle_upload( $file, array( 'test_form' => false ) );
    
    if ( isset( $upload['error'] ) ) {
        return new WP_Error( 'upload_error', $upload['error'] );
    }
    
    return $upload;
}
```

### 7.8 AJAX Security

```php
// Register AJAX handlers
add_action( 'wp_ajax_my_plugin_action', 'my_plugin_ajax_handler' );
add_action( 'wp_ajax_nopriv_my_plugin_action', 'my_plugin_ajax_handler' ); // For non-logged-in users

function my_plugin_ajax_handler() {
    // Verify nonce
    check_ajax_referer( 'my_plugin_nonce', 'security' );
    
    // Check capability
    if ( ! current_user_can( 'edit_posts' ) ) {
        wp_send_json_error( array( 'message' => 'Permission denied' ) );
    }
    
    // Sanitize input
    $data = isset( $_POST['data'] ) ? sanitize_text_field( wp_unslash( $_POST['data'] ) ) : '';
    
    // Process and respond
    $result = my_plugin_process_data( $data );
    
    if ( $result ) {
        wp_send_json_success( array( 'data' => $result ) );
    } else {
        wp_send_json_error( array( 'message' => 'Processing failed' ) );
    }
}

// JavaScript side
jQuery(document).ready(function($) {
    $.ajax({
        url: ajaxurl,
        type: 'POST',
        data: {
            action: 'my_plugin_action',
            security: my_plugin_vars.nonce,  // Localized nonce
            data: 'some data'
        },
        success: function(response) {
            if (response.success) {
                console.log(response.data);
            } else {
                console.error(response.data.message);
            }
        }
    });
});
```

---

## 8. Privacy & GDPR Compliance

### 8.1 Data Exporter Registration

```php
/**
 * Register personal data exporter
 */
function my_plugin_register_exporter( $exporters ) {
    $exporters['my-plugin'] = array(
        'exporter_friendly_name' => __( 'My Plugin Data', 'my-plugin' ),
        'callback'               => 'my_plugin_export_personal_data',
    );
    return $exporters;
}
add_filter( 'wp_privacy_personal_data_exporters', 'my_plugin_register_exporter' );

/**
 * Export personal data callback
 */
function my_plugin_export_personal_data( $email_address, $page = 1 ) {
    $export_items = array();
    $user = get_user_by( 'email', $email_address );
    
    if ( $user ) {
        // Get user's data from your plugin
        $user_data = get_user_meta( $user->ID, 'my_plugin_data', true );
        
        if ( $user_data ) {
            $export_items[] = array(
                'group_id'    => 'my-plugin',
                'group_label' => __( 'My Plugin Data', 'my-plugin' ),
                'item_id'     => "my-plugin-{$user->ID}",
                'data'        => array(
                    array(
                        'name'  => __( 'Preference', 'my-plugin' ),
                        'value' => $user_data['preference'],
                    ),
                    array(
                        'name'  => __( 'Last Activity', 'my-plugin' ),
                        'value' => $user_data['last_activity'],
                    ),
                ),
            );
        }
    }
    
    return array(
        'data' => $export_items,
        'done' => true,  // Set false if paginating
    );
}
```

### 8.2 Data Eraser Registration

```php
/**
 * Register personal data eraser
 */
function my_plugin_register_eraser( $erasers ) {
    $erasers['my-plugin'] = array(
        'eraser_friendly_name' => __( 'My Plugin Data', 'my-plugin' ),
        'callback'             => 'my_plugin_erase_personal_data',
    );
    return $erasers;
}
add_filter( 'wp_privacy_personal_data_erasers', 'my_plugin_register_eraser' );

/**
 * Erase personal data callback
 */
function my_plugin_erase_personal_data( $email_address, $page = 1 ) {
    $items_removed  = 0;
    $items_retained = 0;
    $messages       = array();
    
    $user = get_user_by( 'email', $email_address );
    
    if ( $user ) {
        $deleted = delete_user_meta( $user->ID, 'my_plugin_data' );
        
        if ( $deleted ) {
            $items_removed++;
        } else {
            $items_retained++;
            $messages[] = __( 'Some data could not be removed.', 'my-plugin' );
        }
    }
    
    return array(
        'items_removed'  => $items_removed,
        'items_retained' => $items_retained,
        'messages'       => $messages,
        'done'           => true,
    );
}
```

### 8.3 Privacy Policy Content

```php
/**
 * Add privacy policy content suggestion
 */
function my_plugin_add_privacy_policy_content() {
    if ( ! function_exists( 'wp_add_privacy_policy_content' ) ) {
        return;
    }
    
    $content = sprintf(
        '<h2>%s</h2><p>%s</p><h3>%s</h3><p>%s</p>',
        __( 'My Plugin', 'my-plugin' ),
        __( 'When you use this plugin, we collect the following data:', 'my-plugin' ),
        __( 'Data Collected', 'my-plugin' ),
        __( 'We collect your email address and preferences when you configure the plugin settings. This data is stored locally in your WordPress database and is not transmitted to external services.', 'my-plugin' )
    );
    
    wp_add_privacy_policy_content( 'My Plugin', wp_kses_post( $content ) );
}
add_action( 'admin_init', 'my_plugin_add_privacy_policy_content' );
```

### 8.4 External Services Disclosure

**Required in readme.txt if your plugin connects to ANY external service:**

```
== External Services ==

This plugin connects to the following third-party services:

**Google Analytics**
* Purpose: Website traffic analysis
* Data transmitted: Page views, user interactions, IP addresses
* When transmitted: On every page load when enabled
* Service URL: https://analytics.google.com
* Privacy Policy: https://policies.google.com/privacy
* Terms of Service: https://policies.google.com/terms

**OpenAI API**
* Purpose: AI-powered content generation
* Data transmitted: User prompts and content for processing
* When transmitted: When user initiates AI generation feature
* Service URL: https://api.openai.com
* Privacy Policy: https://openai.com/privacy
* Terms of Service: https://openai.com/terms
```

### 8.5 Consent Implementation

```php
/**
 * Opt-in consent checkbox (must default to unchecked)
 */
function my_plugin_consent_field() {
    $consent = get_option( 'my_plugin_data_consent', 'no' );
    ?>
    <label>
        <input type="checkbox" 
               name="my_plugin_data_consent" 
               value="yes" 
               <?php checked( $consent, 'yes' ); ?>>
        <?php esc_html_e( 'I agree to send anonymous usage data to improve this plugin', 'my-plugin' ); ?>
    </label>
    <p class="description">
        <?php esc_html_e( 'This data helps us understand how the plugin is used and improve it.', 'my-plugin' ); ?>
        <a href="<?php echo esc_url( 'https://example.com/privacy' ); ?>" target="_blank">
            <?php esc_html_e( 'Privacy Policy', 'my-plugin' ); ?>
        </a>
    </p>
    <?php
}

// Only collect data if consent given
function my_plugin_maybe_send_analytics() {
    if ( get_option( 'my_plugin_data_consent', 'no' ) !== 'yes' ) {
        return; // No consent, no data collection
    }
    
    // Proceed with data collection
}
```

---

## 9. Licensing Requirements (GPL)

### 9.1 License Declaration

**Main Plugin File Header:**
```php
/**
 * Plugin Name: My Awesome Plugin
 * ...
 * License:     GPL v2 or later
 * License URI: https://www.gnu.org/licenses/gpl-2.0.html
 */
```

**readme.txt:**
```
License: GPLv2 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html
```

### 9.2 GPL-Compatible Licenses

| License | Compatible with GPLv2 | Notes |
|---------|----------------------|-------|
| GPLv2 | ✅ Yes | Recommended |
| GPLv3 | ✅ Yes | Compatible |
| MIT | ✅ Yes | Permissive |
| BSD (2/3-clause) | ✅ Yes | Permissive |
| Apache 2.0 | ⚠️ GPLv3 only | Not GPLv2 compatible |
| LGPL | ✅ Yes | For libraries |
| Public Domain | ✅ Yes | No restrictions |
| CC0 | ✅ Yes | Public domain equivalent |
| Proprietary | ❌ No | Never allowed |
| Creative Commons (NC/ND) | ❌ No | Non-commercial/No-derivatives not allowed |

### 9.3 What Must Be GPL

**100% of these must be GPL-compatible:**

- All PHP code
- All JavaScript code
- All CSS stylesheets
- All images and icons
- All fonts
- All third-party libraries
- All included frameworks
- Documentation (recommended)

### 9.4 Third-Party Library Verification

```php
/**
 * Document all third-party code in your plugin
 * 
 * /vendor/library-name/
 * License: MIT License
 * Source: https://github.com/example/library
 * Version: 2.1.0
 */
```

**Include a CREDITS.txt or LICENSES.txt:**
```
Third-Party Libraries
=====================

Library Name
------------
Version: 2.1.0
License: MIT
URL: https://github.com/example/library
Copyright (c) 2023 Library Author

[Full MIT License text here]
```

---

## 10. Code Quality Standards

### 10.1 PHP Coding Standards (WPCS)

#### Indentation & Spacing

```php
// ✅ CORRECT - Tabs for indentation
function my_plugin_function( $param1, $param2 ) {
	if ( true === $param1 ) {
		$result = do_something( $param2 );
	}
	return $result;
}

// ❌ WRONG - Spaces for indentation
function my_plugin_function($param1, $param2) {
    if ($param1 === true) {
        $result = do_something($param2);
    }
    return $result;
}
```

#### Brace Style

```php
// ✅ CORRECT - Braces on same line, space before
if ( $condition ) {
	// code
} elseif ( $other_condition ) {
	// code
} else {
	// code
}

// ✅ CORRECT - Always use braces, even for single lines
if ( $condition ) {
	do_something();
}

// ❌ WRONG - No braces for single line
if ( $condition )
	do_something();
```

#### Yoda Conditions

```php
// ✅ CORRECT - Yoda condition (value on left)
if ( true === $value ) {
	// code
}

if ( 'active' === $status ) {
	// code
}

// ❌ WRONG - Variable on left
if ( $value === true ) {
	// code
}
```

#### Array Syntax

```php
// ✅ CORRECT - Long array syntax
$array = array(
	'key1' => 'value1',
	'key2' => 'value2',
	'key3' => array(
		'nested' => 'value',
	),
);

// ❌ WRONG - Short array syntax (PHP 5.4+)
$array = [
	'key1' => 'value1',
	'key2' => 'value2',
];
```

#### Naming Conventions

```php
// Functions and variables: lowercase with underscores
function my_plugin_get_user_data() {}
$user_name = 'John';

// Classes: Capitalized words with underscores
class My_Plugin_Admin_Handler {}

// Constants: Uppercase with underscores
define( 'MY_PLUGIN_VERSION', '1.0.0' );
const MY_PLUGIN_SLUG = 'my-plugin';

// Hooks: lowercase with underscores, prefixed
do_action( 'my_plugin_init' );
apply_filters( 'my_plugin_output', $output );
```

### 10.2 Required Prefixing

All custom code must use a **unique 4-5+ character prefix**:

```php
// ✅ CORRECT - Unique prefix
function myplugin_init() {}
class MyPlugin_Handler {}
define( 'MYPLUGIN_VERSION', '1.0.0' );
do_action( 'myplugin_loaded' );
$myplugin_options = get_option( 'myplugin_settings' );

// ❌ WRONG - Generic or reserved prefixes
function wp_custom_init() {}        // wp_ is reserved
function __init() {}                // __ is reserved
function woo_init() {}              // woo is reserved
function _private_func() {}         // Single underscore reserved
```

#### Reserved Prefixes (Will Cause Rejection)

- `wp_`
- `_` (single underscore)
- `__` (double underscore)
- `WordPress`
- `Woo` / `WooCommerce`
- Any trademarked term

### 10.3 PHP Tags

```php
// ✅ CORRECT - Full PHP tags
<?php
// PHP code here
?>

// ❌ WRONG - Short tags
<?
// PHP code here
?>

// ❌ WRONG - Short echo tags (in some contexts)
<?= $variable ?>

// Files with only PHP should omit closing tag
<?php
// PHP code here
// NO closing ?> tag
```

### 10.4 JavaScript Standards

```javascript
// Use single quotes
var message = 'Hello World';

// Use strict equality
if ( value === 'test' ) {
    // code
}

// Use 'use strict'
( function( $ ) {
    'use strict';
    
    // Your code here
    
} )( jQuery );

// Variable naming: camelCase
var userName = 'John';
var isActive = true;

// Constants: SCREAMING_SNAKE_CASE
var MAX_ITEMS = 100;
var API_ENDPOINT = '/wp-json/my-plugin/v1/';
```

### 10.5 Script & Style Enqueuing

```php
/**
 * Enqueue scripts and styles properly
 */
function my_plugin_enqueue_assets() {
    // Enqueue styles
    wp_enqueue_style(
        'my-plugin-style',
        plugin_dir_url( __FILE__ ) . 'css/style.css',
        array(),  // Dependencies
        MY_PLUGIN_VERSION
    );
    
    // Enqueue scripts with dependencies
    wp_enqueue_script(
        'my-plugin-script',
        plugin_dir_url( __FILE__ ) . 'js/script.js',
        array( 'jquery' ),  // Dependencies - use WordPress bundled jQuery
        MY_PLUGIN_VERSION,
        true  // In footer
    );
    
    // Localize script (pass data to JavaScript)
    wp_localize_script(
        'my-plugin-script',
        'myPluginVars',
        array(
            'ajaxurl' => admin_url( 'admin-ajax.php' ),
            'nonce'   => wp_create_nonce( 'my_plugin_nonce' ),
            'strings' => array(
                'confirm' => __( 'Are you sure?', 'my-plugin' ),
                'error'   => __( 'An error occurred.', 'my-plugin' ),
            ),
        )
    );
}
add_action( 'wp_enqueue_scripts', 'my_plugin_enqueue_assets' );
add_action( 'admin_enqueue_scripts', 'my_plugin_enqueue_admin_assets' );
```

### 10.6 WordPress Bundled Libraries

**MUST use WordPress bundled versions - DO NOT include your own:**

| Library | WordPress Handle |
|---------|------------------|
| jQuery | `jquery` |
| jQuery UI | `jquery-ui-core`, `jquery-ui-dialog`, etc. |
| Backbone.js | `backbone` |
| Underscore.js | `underscore` |
| React | `react`, `react-dom` |
| Lodash | `lodash` |
| Moment.js | `moment` |
| PHPMailer | (use `wp_mail()`) |
| SimplePie | (use `fetch_feed()`) |
| Requests | (use `wp_remote_*()`) |

---

## 11. Internationalization (i18n)

### 11.1 Text Domain Rules

```php
// Text domain MUST match plugin slug exactly
// Plugin slug: my-awesome-plugin
// Text domain: my-awesome-plugin (NOT my_awesome_plugin)

// ✅ CORRECT
__( 'Hello World', 'my-awesome-plugin' );

// ❌ WRONG - underscore instead of hyphen
__( 'Hello World', 'my_awesome_plugin' );

// ❌ WRONG - variable text domain (breaks string extraction)
$domain = 'my-awesome-plugin';
__( 'Hello World', $domain );
```

### 11.2 Translation Functions

```php
// Basic translation
$text = __( 'Hello World', 'my-plugin' );

// Echo translated text
_e( 'Hello World', 'my-plugin' );

// Translation with context
$text = _x( 'Post', 'noun', 'my-plugin' );
_ex( 'Post', 'noun', 'my-plugin' );

// Singular/plural
$text = _n( '%d item', '%d items', $count, 'my-plugin' );
printf( _n( '%d item', '%d items', $count, 'my-plugin' ), $count );

// Escaped translations (recommended for output)
echo esc_html__( 'Hello World', 'my-plugin' );
esc_html_e( 'Hello World', 'my-plugin' );
echo esc_attr__( 'Button text', 'my-plugin' );
esc_attr_e( 'Button text', 'my-plugin' );
```

### 11.3 Loading Text Domain

```php
/**
 * Load plugin text domain
 */
function my_plugin_load_textdomain() {
    load_plugin_textdomain(
        'my-plugin',
        false,
        dirname( plugin_basename( __FILE__ ) ) . '/languages'
    );
}
add_action( 'plugins_loaded', 'my_plugin_load_textdomain' );
```

### 11.4 Translator Comments

```php
// Provide context for translators
/* translators: %s: User name */
$message = sprintf( __( 'Hello, %s!', 'my-plugin' ), $user_name );

/* translators: 1: Start date, 2: End date */
$range = sprintf(
    __( 'From %1$s to %2$s', 'my-plugin' ),
    $start_date,
    $end_date
);
```

---

## 12. Accessibility Standards

### 12.1 Requirements (WCAG 2.2 Level AA)

| Requirement | Standard |
|-------------|----------|
| Color Contrast (normal text) | 4.5:1 minimum |
| Color Contrast (large text) | 3:1 minimum |
| Keyboard Navigation | All interactive elements |
| Focus Indicators | Visible on all focusable elements |
| Form Labels | Every input must have label |
| Alt Text | All meaningful images |
| Heading Hierarchy | Logical order (h1 → h2 → h3) |
| Skip Links | For navigation-heavy pages |

### 12.2 Accessible Form Example

```php
<form method="post" action="">
    <?php wp_nonce_field( 'my_plugin_save', 'my_plugin_nonce' ); ?>
    
    <fieldset>
        <legend><?php esc_html_e( 'User Settings', 'my-plugin' ); ?></legend>
        
        <!-- Text input with label -->
        <p>
            <label for="my-plugin-name">
                <?php esc_html_e( 'Name', 'my-plugin' ); ?>
                <span class="required" aria-hidden="true">*</span>
                <span class="screen-reader-text"><?php esc_html_e( '(required)', 'my-plugin' ); ?></span>
            </label>
            <input type="text" 
                   id="my-plugin-name" 
                   name="name" 
                   required
                   aria-required="true"
                   value="<?php echo esc_attr( $name ); ?>">
        </p>
        
        <!-- Select with label -->
        <p>
            <label for="my-plugin-country">
                <?php esc_html_e( 'Country', 'my-plugin' ); ?>
            </label>
            <select id="my-plugin-country" name="country">
                <option value=""><?php esc_html_e( 'Select a country', 'my-plugin' ); ?></option>
                <!-- options -->
            </select>
        </p>
        
        <!-- Checkbox with label -->
        <p>
            <input type="checkbox" 
                   id="my-plugin-subscribe" 
                   name="subscribe" 
                   value="1">
            <label for="my-plugin-subscribe">
                <?php esc_html_e( 'Subscribe to newsletter', 'my-plugin' ); ?>
            </label>
        </p>
    </fieldset>
    
    <!-- Submit button with clear text -->
    <p>
        <button type="submit" class="button button-primary">
            <?php esc_html_e( 'Save Settings', 'my-plugin' ); ?>
        </button>
    </p>
</form>
```

### 12.3 ARIA Attributes Usage

```html
<!-- Live regions for dynamic content -->
<div id="notification" aria-live="polite" aria-atomic="true"></div>

<!-- Expandable sections -->
<button aria-expanded="false" aria-controls="section-1">
    Toggle Section
</button>
<div id="section-1" hidden>
    Section content
</div>

<!-- Loading states -->
<div aria-busy="true" aria-live="polite">
    Loading...
</div>

<!-- Error messages -->
<input type="email" 
       id="email" 
       aria-describedby="email-error"
       aria-invalid="true">
<span id="email-error" role="alert">
    Please enter a valid email address.
</span>
```

---

## 13. Prohibited Practices

### 13.1 Banned Code Patterns

```php
// ❌ BANNED - eval() and similar
eval( $code );
create_function( '$a', 'return $a;' );  // Deprecated PHP 7.2, removed 8.0
assert( $code );  // When used for code execution

// ❌ BANNED - Obfuscation patterns
base64_decode( 'encoded_executable_code' );
gzinflate( base64_decode( $data ) );  // Common malware pattern
str_rot13( $code );  // For hiding code

// ❌ BANNED - Direct shell execution
`ls -la`;
shell_exec( $command );
exec( $command );
system( $command );
passthru( $command );
proc_open( $command, $descriptors, $pipes );

// ❌ BANNED - Error suppression
$result = @file_get_contents( $url );

// ❌ BANNED - goto statement
goto label;

// ❌ BANNED - extract() function
extract( $_POST );

// ❌ BANNED - preg_replace /e modifier
preg_replace( '/pattern/e', 'code', $subject );

// ❌ BANNED - Variable variables with user input
$user_input = $_GET['var'];
$$user_input = 'value';

// ❌ BANNED - Including remote files
include( 'http://example.com/file.php' );
require( $_GET['file'] );
```

### 13.2 Obfuscated Code

**Guideline 4 requires "mostly human readable" code:**

```php
// ❌ BANNED - Base64 encoded executable code
$code = base64_decode('ZWNobyAiSGVsbG8gV29ybGQiOw==');
eval($code);

// ❌ BANNED - p,a,c,k,e,r obfuscation
eval(function(p,a,c,k,e,r){...}('encoded|data|here',4,4,'...'.split('|')));

// ❌ BANNED - Deliberately unclear naming
function _0x4a2b($_0x3c1d, $_0x2e4f) {
    return $_0x3c1d + $_0x2e4f;
}

// ✅ ALLOWED - Minified code WITH source available
// script.min.js must have script.js available (included or linked)
```

### 13.3 Direct File Loading

```php
// ❌ BANNED - Loading wp-load.php directly
require_once( '../../../wp-load.php' );

// ❌ BANNED - Direct script tags
echo '<script src="https://cdn.example.com/script.js"></script>';

// ✅ CORRECT - Use WordPress functions
wp_enqueue_script( 'my-script', plugin_dir_url(__FILE__) . 'js/script.js' );
```

### 13.4 External Resource Restrictions

```php
// ❌ BANNED - Loading scripts from CDNs (except fonts)
wp_enqueue_script( 'jquery', 'https://cdn.jsdelivr.net/npm/jquery@3/dist/jquery.min.js' );

// ❌ BANNED - Loading CSS from CDNs (except fonts)
wp_enqueue_style( 'bootstrap', 'https://cdn.jsdelivr.net/npm/bootstrap@5/dist/css/bootstrap.min.css' );

// ✅ ALLOWED - Google Fonts
wp_enqueue_style( 'google-fonts', 'https://fonts.googleapis.com/css2?family=Roboto&display=swap' );

// ❌ BANNED - Serving plugin updates from external server
// WordPress.org MUST be the update source
```

### 13.5 Banned HTTP Methods

```php
// ❌ BANNED - Direct cURL usage
$ch = curl_init();
curl_setopt( $ch, CURLOPT_URL, $url );
$response = curl_exec( $ch );

// ❌ BANNED - Direct file_get_contents for URLs
$data = file_get_contents( 'https://api.example.com/data' );

// ✅ CORRECT - Use WordPress HTTP API
$response = wp_remote_get( 'https://api.example.com/data' );
$response = wp_remote_post( $url, array( 'body' => $data ) );

if ( is_wp_error( $response ) ) {
    // Handle error
} else {
    $body = wp_remote_retrieve_body( $response );
}
```

---

## 14. Commercial & Freemium Rules

### 14.1 Guideline 5: Trialware Prohibition

**The following are BANNED:**

| Prohibited | Description |
|------------|-------------|
| Locked Features | Features visible but requiring payment |
| Trial Expirations | Functionality that stops working after time period |
| Usage Quotas | Limiting actions until user pays |
| Nag Screens | Persistent upgrade prompts site-wide |
| Fake Limitations | Artificial restrictions to force upgrade |

### 14.2 Permitted Freemium Model

```
WordPress.org Version (FREE):
├── Full, complete functionality
├── No artificial limitations
├── All advertised features work
└── Valuable standalone product

Separately Sold (NOT on WordPress.org):
├── Additional features/add-ons
├── Priority support
├── Advanced integrations
└── White-label options
```

### 14.3 Acceptable Upselling

```php
/**
 * Upselling rules:
 * 1. Only on YOUR plugin's settings page
 * 2. Must be dismissible
 * 3. Cannot appear site-wide
 * 4. Cannot block functionality
 */

// ✅ ACCEPTABLE - On plugin's own settings page, dismissible
function my_plugin_admin_notice() {
    $screen = get_current_screen();
    
    // Only show on plugin's settings page
    if ( 'settings_page_my-plugin' !== $screen->id ) {
        return;
    }
    
    // Check if dismissed
    if ( get_option( 'my_plugin_promo_dismissed' ) ) {
        return;
    }
    
    ?>
    <div class="notice notice-info is-dismissible" data-notice="my-plugin-promo">
        <p>
            <?php esc_html_e( 'Upgrade to Pro for advanced features!', 'my-plugin' ); ?>
            <a href="https://example.com/pro"><?php esc_html_e( 'Learn More', 'my-plugin' ); ?></a>
        </p>
    </div>
    <?php
}
add_action( 'admin_notices', 'my_plugin_admin_notice' );

// ❌ BANNED - Site-wide notices
function bad_plugin_notice() {
    // This would show on ALL admin pages - NOT ALLOWED
    echo '<div class="notice">Buy our premium version!</div>';
}
```

### 14.4 Affiliate Links

```php
// ✅ ALLOWED - In readme.txt
// You can include affiliate links in readme.txt description

// ❌ BANNED - Injected affiliate links
// Cannot automatically add affiliate parameters to links
// Cannot modify user content to include affiliate codes
```

---

## 15. External Services & API Rules

### 15.1 Guideline 7: Consent Requirements

```
External Service Connection Rules:

1. MUST disclose in readme.txt
2. User MUST take action to enable (opt-in)
3. Service MUST provide "functionality of substance"
4. CANNOT be purely for license validation
5. CANNOT collect data without consent
```

### 15.2 Acceptable External Connections

```php
// ✅ ALLOWED - SaaS with substantial functionality
// - API integrations (Twitter, Google, OpenAI)
// - CDN services for user-uploaded content
// - Payment gateways (Stripe, PayPal)
// - Email services (Mailchimp, SendGrid)

// ✅ ALLOWED - With explicit opt-in
function my_plugin_analytics_optin() {
    // Only if user explicitly enabled
    if ( 'yes' !== get_option( 'my_plugin_analytics_consent' ) ) {
        return;
    }
    
    // Send anonymous analytics
    wp_remote_post( 'https://analytics.myplugin.com/collect', array(
        'body' => array(
            'wp_version' => get_bloginfo( 'version' ),
            'php_version' => phpversion(),
            'plugin_version' => MY_PLUGIN_VERSION,
        ),
    ) );
}
```

### 15.3 Prohibited External Connections

```php
// ❌ BANNED - License-only validation
function check_license() {
    // Cannot lock features behind external license check
    $response = wp_remote_get( 'https://licenses.example.com/validate/' . $key );
    if ( ! valid ) {
        disable_premium_features();  // NOT ALLOWED
    }
}

// ❌ BANNED - Auto data collection without consent
function my_plugin_init() {
    // Cannot automatically send data
    wp_remote_post( 'https://tracking.example.com', array(
        'body' => array(
            'site_url' => get_site_url(),
            'admin_email' => get_option( 'admin_email' ),
        ),
    ) );
}

// ❌ BANNED - Loading admin UI from external source
function my_plugin_admin_page() {
    // Cannot iframe external admin panels
    echo '<iframe src="https://dashboard.example.com"></iframe>';
}
```

---

## 16. Block Plugins (Block Directory)

### 16.1 Additional Requirements

Block plugins submitted to the Block Directory face **stricter rules**:

| Requirement | Standard |
|-------------|----------|
| Single block focus | One block per plugin (recommended) |
| No payment | Block functionality cannot require payment |
| No upselling in blocks | No upgrade prompts within block UI |
| No advertisements | No ads within blocks |
| Server rendering | Must work without JavaScript for SSR |
| Block.json required | Must include block.json metadata |

### 16.2 Block.json Template

```json
{
    "$schema": "https://schemas.wp.org/trunk/block.json",
    "apiVersion": 3,
    "name": "my-plugin/my-block",
    "version": "1.0.0",
    "title": "My Custom Block",
    "category": "widgets",
    "icon": "smiley",
    "description": "A custom block for displaying content.",
    "keywords": [ "custom", "content", "display" ],
    "supports": {
        "html": false,
        "align": [ "wide", "full" ],
        "color": {
            "background": true,
            "text": true
        }
    },
    "textdomain": "my-plugin",
    "editorScript": "file:./build/index.js",
    "editorStyle": "file:./build/index.css",
    "style": "file:./build/style-index.css",
    "render": "file:./render.php"
}
```

---

## 17. Common Rejection Reasons

### 17.1 Security Issues (~80% of rejections)

| Issue | Solution |
|-------|----------|
| Missing sanitization | Use appropriate `sanitize_*()` functions |
| Missing escaping | Escape at output with `esc_*()` functions |
| Missing nonce verification | Add `wp_nonce_field()` and `wp_verify_nonce()` |
| Missing capability checks | Add `current_user_can()` checks |
| SQL injection vulnerabilities | Use `$wpdb->prepare()` |
| Direct file access | Add `ABSPATH` check to all PHP files |

### 17.2 Code Quality Issues

| Issue | Solution |
|-------|----------|
| Included WordPress libraries | Remove and use bundled versions |
| Development files included | Remove node_modules, vendor, tests, etc. |
| Obfuscated code | Provide readable source code |
| Missing text domain | Add proper text domain to all strings |
| Generic prefixes | Use unique 4+ character prefix |
| WP_DEBUG errors | Test with `WP_DEBUG` enabled |

### 17.3 Licensing Issues

| Issue | Solution |
|-------|----------|
| Missing license declaration | Add license to header and readme |
| Incompatible library | Replace with GPL-compatible alternative |
| Trademark violations | Rename to avoid trademarks |
| Split licensing | Ensure 100% GPL compatibility |

### 17.4 Documentation Issues

| Issue | Solution |
|-------|----------|
| Invalid readme.txt | Validate at WordPress.org validator |
| Missing external service disclosure | Add External Services section |
| Stable tag mismatch | Ensure stable tag matches version folder |
| Missing changelog | Add detailed changelog section |

---

## 18. Pre-Submission Checklist

### 18.1 Security Checklist

```
□ All $_POST/$_GET/$_REQUEST/$_FILES data sanitized
□ All echoed variables escaped with correct esc_* function
□ Nonces implemented for all forms and AJAX
□ Nonces verified before processing
□ Capability checks before privileged operations
□ $wpdb->prepare() used for all queries with variables
□ Direct file access prevented (ABSPATH check)
□ No eval(), create_function(), or shell execution
□ File uploads validated and sanitized
□ AJAX handlers secured with nonce + capability
```

### 18.2 Code Quality Checklist

```
□ Unique prefix (4+ chars) on functions, classes, hooks
□ No WordPress core libraries included
□ Using wp_enqueue_script/style() for all assets
□ Using WordPress HTTP API (not cURL)
□ WPCS coding standards followed
□ No PHP errors with WP_DEBUG enabled
□ No JavaScript errors in console
□ Text domain matches plugin slug exactly
□ All strings internationalized
□ Minified files have source available
```

### 18.3 Documentation Checklist

```
□ readme.txt validates at wordpress.org/plugins/developers/readme-validator/
□ Stable tag matches version in main plugin file
□ All required readme sections present
□ External services documented with privacy/terms links
□ Changelog is detailed and current
□ License declared in header AND readme.txt
□ Screenshots added to /assets/ folder
□ Clear installation instructions
□ FAQ addresses common questions
```

### 18.4 File Structure Checklist

```
□ Main plugin file in root of /trunk/
□ No development files (node_modules, vendor, tests, .git)
□ ZIP file under 10MB
□ Folder name matches plugin slug
□ All PHP files have ABSPATH check
□ Language files in /languages/ folder
□ composer.json included if using Composer
□ uninstall.php for clean removal (recommended)
```

### 18.5 Pre-Submission Testing

```
□ Plugin Check (PCP) passes all categories:
  □ Security
  □ Performance  
  □ Accessibility
  □ Plugin Repo
□ Tested on latest WordPress version
□ Tested on minimum declared WordPress version
□ Tested on minimum declared PHP version
□ Tested with popular themes (Twenty Twenty-*)
□ Tested with common plugins (Yoast, WooCommerce)
□ Multisite compatibility tested (if applicable)
```

---

## 19. Tools & Resources

### 19.1 Official Resources

| Resource | URL |
|----------|-----|
| Plugin Developer Handbook | https://developer.wordpress.org/plugins/ |
| Detailed Plugin Guidelines | https://developer.wordpress.org/plugins/wordpress-org/detailed-plugin-guidelines/ |
| Plugin Developer FAQ | https://developer.wordpress.org/plugins/wordpress-org/plugin-developer-faq/ |
| Common Issues | https://developer.wordpress.org/plugins/wordpress-org/common-issues/ |
| Security APIs | https://developer.wordpress.org/apis/security/ |
| Readme Validator | https://wordpress.org/plugins/developers/readme-validator/ |
| Submit a Plugin | https://wordpress.org/plugins/developers/add/ |

### 19.2 Development Tools

| Tool | Purpose |
|------|---------|
| Plugin Check (PCP) | https://wordpress.org/plugins/plugin-check/ |
| WordPress Coding Standards | https://github.com/WordPress/WordPress-Coding-Standards |
| PHP_CodeSniffer | https://github.com/squizlabs/PHP_CodeSniffer |
| WP-CLI | https://wp-cli.org/ |
| Health Check Plugin | https://wordpress.org/plugins/health-check/ |
| Query Monitor | https://wordpress.org/plugins/query-monitor/ |

### 19.3 Communication Channels

| Channel | Purpose |
|---------|---------|
| plugins@wordpress.org | Review team communication (7 business day response) |
| #pluginreview (Slack) | Real-time discussion |
| Make WordPress Plugins | https://make.wordpress.org/plugins/ (announcements) |
| WordPress Stack Exchange | Community Q&A |

### 19.4 GitHub Actions for CI/CD

```yaml
# .github/workflows/plugin-check.yml
name: Plugin Check

on: [push, pull_request]

jobs:
  plugin-check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Run Plugin Check
        uses: wordpress/plugin-check-action@v1
        with:
          categories: |
            security
            performance
            plugin_repo
```

---

## 20. Code Examples & Templates

### 20.1 Complete Main Plugin File Template

```php
<?php
/**
 * Plugin Name:       My Awesome Plugin
 * Plugin URI:        https://example.com/my-awesome-plugin
 * Description:       A comprehensive WordPress plugin following all best practices.
 * Version:           1.0.0
 * Requires at least: 6.0
 * Requires PHP:      7.4
 * Author:            Your Name
 * Author URI:        https://example.com
 * License:           GPL v2 or later
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain:       my-awesome-plugin
 * Domain Path:       /languages
 *
 * @package MyAwesomePlugin
 */

// Prevent direct access
if ( ! defined( 'ABSPATH' ) ) {
	exit;
}

// Define plugin constants
define( 'MY_AWESOME_PLUGIN_VERSION', '1.0.0' );
define( 'MY_AWESOME_PLUGIN_PATH', plugin_dir_path( __FILE__ ) );
define( 'MY_AWESOME_PLUGIN_URL', plugin_dir_url( __FILE__ ) );
define( 'MY_AWESOME_PLUGIN_BASENAME', plugin_basename( __FILE__ ) );

/**
 * Load plugin text domain for translations
 */
function my_awesome_plugin_load_textdomain() {
	load_plugin_textdomain(
		'my-awesome-plugin',
		false,
		dirname( MY_AWESOME_PLUGIN_BASENAME ) . '/languages'
	);
}
add_action( 'plugins_loaded', 'my_awesome_plugin_load_textdomain' );

/**
 * Activation hook
 */
function my_awesome_plugin_activate() {
	// Create database tables, set default options, etc.
	add_option( 'my_awesome_plugin_version', MY_AWESOME_PLUGIN_VERSION );
	
	// Flush rewrite rules if needed
	flush_rewrite_rules();
}
register_activation_hook( __FILE__, 'my_awesome_plugin_activate' );

/**
 * Deactivation hook
 */
function my_awesome_plugin_deactivate() {
	// Cleanup temporary data
	flush_rewrite_rules();
}
register_deactivation_hook( __FILE__, 'my_awesome_plugin_deactivate' );

/**
 * Initialize plugin
 */
function my_awesome_plugin_init() {
	// Load required files
	require_once MY_AWESOME_PLUGIN_PATH . 'includes/class-my-awesome-plugin.php';
	
	// Initialize main class
	$plugin = new My_Awesome_Plugin();
	$plugin->run();
}
add_action( 'plugins_loaded', 'my_awesome_plugin_init' );

/**
 * Enqueue frontend scripts and styles
 */
function my_awesome_plugin_enqueue_assets() {
	wp_enqueue_style(
		'my-awesome-plugin-style',
		MY_AWESOME_PLUGIN_URL . 'assets/css/frontend.css',
		array(),
		MY_AWESOME_PLUGIN_VERSION
	);
	
	wp_enqueue_script(
		'my-awesome-plugin-script',
		MY_AWESOME_PLUGIN_URL . 'assets/js/frontend.js',
		array( 'jquery' ),
		MY_AWESOME_PLUGIN_VERSION,
		true
	);
	
	wp_localize_script(
		'my-awesome-plugin-script',
		'myAwesomePluginVars',
		array(
			'ajaxurl' => admin_url( 'admin-ajax.php' ),
			'nonce'   => wp_create_nonce( 'my_awesome_plugin_nonce' ),
		)
	);
}
add_action( 'wp_enqueue_scripts', 'my_awesome_plugin_enqueue_assets' );

/**
 * Enqueue admin scripts and styles
 */
function my_awesome_plugin_admin_enqueue_assets( $hook ) {
	// Only load on plugin pages
	if ( 'settings_page_my-awesome-plugin' !== $hook ) {
		return;
	}
	
	wp_enqueue_style(
		'my-awesome-plugin-admin-style',
		MY_AWESOME_PLUGIN_URL . 'assets/css/admin.css',
		array(),
		MY_AWESOME_PLUGIN_VERSION
	);
	
	wp_enqueue_script(
		'my-awesome-plugin-admin-script',
		MY_AWESOME_PLUGIN_URL . 'assets/js/admin.js',
		array( 'jquery' ),
		MY_AWESOME_PLUGIN_VERSION,
		true
	);
}
add_action( 'admin_enqueue_scripts', 'my_awesome_plugin_admin_enqueue_assets' );

/**
 * Add settings page
 */
function my_awesome_plugin_add_menu() {
	add_options_page(
		__( 'My Awesome Plugin Settings', 'my-awesome-plugin' ),
		__( 'My Awesome Plugin', 'my-awesome-plugin' ),
		'manage_options',
		'my-awesome-plugin',
		'my_awesome_plugin_settings_page'
	);
}
add_action( 'admin_menu', 'my_awesome_plugin_add_menu' );

/**
 * Settings page callback
 */
function my_awesome_plugin_settings_page() {
	// Check user capability
	if ( ! current_user_can( 'manage_options' ) ) {
		return;
	}
	
	include MY_AWESOME_PLUGIN_PATH . 'admin/settings-page.php';
}

/**
 * AJAX handler example
 */
function my_awesome_plugin_ajax_handler() {
	// Verify nonce
	check_ajax_referer( 'my_awesome_plugin_nonce', 'security' );
	
	// Check capability
	if ( ! current_user_can( 'edit_posts' ) ) {
		wp_send_json_error( array( 'message' => __( 'Permission denied.', 'my-awesome-plugin' ) ) );
	}
	
	// Sanitize input
	$data = isset( $_POST['data'] ) ? sanitize_text_field( wp_unslash( $_POST['data'] ) ) : '';
	
	// Process and respond
	wp_send_json_success( array( 'result' => $data ) );
}
add_action( 'wp_ajax_my_awesome_plugin_action', 'my_awesome_plugin_ajax_handler' );
```

### 20.2 Uninstall.php Template

```php
<?php
/**
 * Uninstall handler - runs when plugin is deleted
 *
 * @package MyAwesomePlugin
 */

// If uninstall not called from WordPress, exit
if ( ! defined( 'WP_UNINSTALL_PLUGIN' ) ) {
	exit;
}

// Delete options
delete_option( 'my_awesome_plugin_version' );
delete_option( 'my_awesome_plugin_settings' );

// Delete options from multisite
if ( is_multisite() ) {
	delete_site_option( 'my_awesome_plugin_version' );
	
	// Get all sites
	$sites = get_sites( array( 'fields' => 'ids' ) );
	foreach ( $sites as $site_id ) {
		switch_to_blog( $site_id );
		delete_option( 'my_awesome_plugin_settings' );
		restore_current_blog();
	}
}

// Delete user meta
delete_metadata( 'user', 0, 'my_awesome_plugin_user_data', '', true );

// Delete custom tables
global $wpdb;
$wpdb->query( "DROP TABLE IF EXISTS {$wpdb->prefix}my_awesome_plugin_data" );

// Clear scheduled hooks
wp_clear_scheduled_hook( 'my_awesome_plugin_cron_event' );

// Clear transients
delete_transient( 'my_awesome_plugin_cache' );

// Clear any cached data
wp_cache_flush();
```

### 20.3 Settings Form Template

```php
<?php
/**
 * Settings page template
 *
 * @package MyAwesomePlugin
 */

// Prevent direct access
if ( ! defined( 'ABSPATH' ) ) {
	exit;
}

// Handle form submission
if ( isset( $_POST['my_awesome_plugin_save'] ) ) {
	// Verify nonce
	if ( ! isset( $_POST['my_awesome_plugin_nonce'] ) ||
		 ! wp_verify_nonce( sanitize_text_field( wp_unslash( $_POST['my_awesome_plugin_nonce'] ) ), 'my_awesome_plugin_settings' ) ) {
		wp_die( esc_html__( 'Security check failed.', 'my-awesome-plugin' ) );
	}
	
	// Check capability
	if ( ! current_user_can( 'manage_options' ) ) {
		wp_die( esc_html__( 'Permission denied.', 'my-awesome-plugin' ) );
	}
	
	// Sanitize and save options
	$settings = array(
		'enable_feature' => isset( $_POST['enable_feature'] ) ? 'yes' : 'no',
		'api_key'        => isset( $_POST['api_key'] ) ? sanitize_text_field( wp_unslash( $_POST['api_key'] ) ) : '',
		'max_items'      => isset( $_POST['max_items'] ) ? absint( $_POST['max_items'] ) : 10,
		'email'          => isset( $_POST['email'] ) ? sanitize_email( wp_unslash( $_POST['email'] ) ) : '',
	);
	
	update_option( 'my_awesome_plugin_settings', $settings );
	
	echo '<div class="notice notice-success is-dismissible"><p>' . esc_html__( 'Settings saved.', 'my-awesome-plugin' ) . '</p></div>';
}

// Get current settings
$settings = get_option( 'my_awesome_plugin_settings', array(
	'enable_feature' => 'no',
	'api_key'        => '',
	'max_items'      => 10,
	'email'          => '',
) );
?>

<div class="wrap">
	<h1><?php echo esc_html( get_admin_page_title() ); ?></h1>
	
	<form method="post" action="">
		<?php wp_nonce_field( 'my_awesome_plugin_settings', 'my_awesome_plugin_nonce' ); ?>
		
		<table class="form-table" role="presentation">
			<tbody>
				<tr>
					<th scope="row">
						<label for="enable_feature">
							<?php esc_html_e( 'Enable Feature', 'my-awesome-plugin' ); ?>
						</label>
					</th>
					<td>
						<input type="checkbox" 
							   id="enable_feature" 
							   name="enable_feature" 
							   value="yes" 
							   <?php checked( $settings['enable_feature'], 'yes' ); ?>>
						<p class="description">
							<?php esc_html_e( 'Enable the main feature of this plugin.', 'my-awesome-plugin' ); ?>
						</p>
					</td>
				</tr>
				
				<tr>
					<th scope="row">
						<label for="api_key">
							<?php esc_html_e( 'API Key', 'my-awesome-plugin' ); ?>
						</label>
					</th>
					<td>
						<input type="text" 
							   id="api_key" 
							   name="api_key" 
							   value="<?php echo esc_attr( $settings['api_key'] ); ?>" 
							   class="regular-text">
						<p class="description">
							<?php esc_html_e( 'Enter your API key from the service provider.', 'my-awesome-plugin' ); ?>
						</p>
					</td>
				</tr>
				
				<tr>
					<th scope="row">
						<label for="max_items">
							<?php esc_html_e( 'Maximum Items', 'my-awesome-plugin' ); ?>
						</label>
					</th>
					<td>
						<input type="number" 
							   id="max_items" 
							   name="max_items" 
							   value="<?php echo esc_attr( $settings['max_items'] ); ?>" 
							   min="1" 
							   max="100" 
							   class="small-text">
						<p class="description">
							<?php esc_html_e( 'Maximum number of items to display (1-100).', 'my-awesome-plugin' ); ?>
						</p>
					</td>
				</tr>
				
				<tr>
					<th scope="row">
						<label for="email">
							<?php esc_html_e( 'Notification Email', 'my-awesome-plugin' ); ?>
						</label>
					</th>
					<td>
						<input type="email" 
							   id="email" 
							   name="email" 
							   value="<?php echo esc_attr( $settings['email'] ); ?>" 
							   class="regular-text">
						<p class="description">
							<?php esc_html_e( 'Email address for notifications.', 'my-awesome-plugin' ); ?>
						</p>
					</td>
				</tr>
			</tbody>
		</table>
		
		<?php submit_button( __( 'Save Settings', 'my-awesome-plugin' ), 'primary', 'my_awesome_plugin_save' ); ?>
	</form>
</div>
```

---

## Quick Reference Card

### Must-Have Security Pattern

```php
// 1. Verify nonce
if ( ! wp_verify_nonce( $_POST['nonce'], 'action' ) ) { die(); }

// 2. Check capability
if ( ! current_user_can( 'manage_options' ) ) { die(); }

// 3. Sanitize input
$data = sanitize_text_field( wp_unslash( $_POST['data'] ) );

// 4. Escape output
echo esc_html( $data );
```

### Essential Functions Cheat Sheet

| Input Type | Sanitize | Escape |
|------------|----------|--------|
| Text | `sanitize_text_field()` | `esc_html()` |
| HTML | `wp_kses_post()` | `wp_kses_post()` |
| URL | `esc_url_raw()` | `esc_url()` |
| Email | `sanitize_email()` | `esc_attr()` |
| Integer | `absint()` | `intval()` |
| Attribute | `sanitize_text_field()` | `esc_attr()` |
| JS | `sanitize_text_field()` | `esc_js()` |

### File Header Quick Template

```php
<?php
/**
 * Plugin Name: Plugin Name
 * Version:     1.0.0
 * License:     GPL v2 or later
 * Text Domain: plugin-name
 */
if ( ! defined( 'ABSPATH' ) ) exit;
```

---

## Document Information

**Version:** 1.0.0  
**Last Updated:** December 2024  
**Sources:** WordPress.org Plugin Handbook, Make WordPress Plugins, WordPress Stack Exchange, Community Developer Blogs

**Official Links:**

- Plugin Handbook: https://developer.wordpress.org/plugins/
- Submit Plugin: https://wordpress.org/plugins/developers/add/
- Plugin Check: https://wordpress.org/plugins/plugin-check/
- Readme Validator: https://wordpress.org/plugins/developers/readme-validator/

> **Document prepared for NexaLance WordPress Plugin Development**

---

*This document is provided for reference purposes. Always check the official WordPress.org documentation for the most current requirements.*

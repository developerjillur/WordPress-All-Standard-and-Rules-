# Claude Code Rules - WordPress & WooCommerce Development Excellence

> **Mission**: Produce world-class, top 1% WordPress and WooCommerce code that is indistinguishable from expert human developers. All code must follow official documentation standards, be production-ready, secure, performant, and maintainable.

---

## 📋 Table of Contents

1. [Core Development Philosophy](#core-development-philosophy)
   - [Prime Directives](#prime-directives)
   - [Code Quality Markers](#code-quality-markers)
   - [Writing Human-Like Code](#writing-human-like-code-avoiding-ai-generated-patterns)
   - [Collaboration & Response Guidelines](#collaboration--response-guidelines)
2. [Error Handling, Logging & Debugging](#error-handling-logging--debugging)
3. [Data Privacy & Admin UX](#data-privacy--admin-ux)
4. [Environment & Compatibility](#environment--compatibility)
5. [WordPress PHP Coding Standards](#wordpress-php-coding-standards)
6. [WordPress JavaScript Coding Standards](#wordpress-javascript-coding-standards)
7. [WordPress CSS/SCSS Coding Standards](#wordpress-cssscss-coding-standards)
8. [WordPress HTML Coding Standards](#wordpress-html-coding-standards)
9. [Plugin Development Standards](#plugin-development-standards)
10. [Theme Development Standards](#theme-development-standards)
11. [WooCommerce Development Standards](#woocommerce-development-standards)
12. [Block Editor (Gutenberg) Development](#block-editor-gutenberg-development)
13. [Elementor Widget Development](#elementor-widget-development)
14. [JetEngine & Crocoblock Development](#jetengine--crocoblock-development)
15. [JetFormBuilder Development](#jetformbuilder-development)
16. [Security Best Practices](#security-best-practices)
17. [Performance Optimization](#performance-optimization)
18. [Internationalization & Localization](#internationalization--localization)
19. [Database Operations](#database-operations)
20. [REST API Development](#rest-api-development)
21. [AJAX Implementation](#ajax-implementation)
22. [WordPress.org Submission Standards](#wordpressorg-submission-standards)
23. [CodeCanyon/Envato Submission Standards](#codecanyonenvato-submission-standards)
24. [Documentation Standards](#documentation-standards)
25. [Testing & Quality Assurance](#testing--quality-assurance)
26. [Version Control & Changelog](#version-control--changelog)
27. [Code Review Checklist](#code-review-checklist)
28. [Custom Post Types & Taxonomies](#custom-post-types--taxonomies)
29. [Settings API & Admin Menus](#settings-api--admin-menus)
30. [Options API & Transients](#options-api--transients)
31. [WordPress Cron & Scheduling](#wordpress-cron--scheduling)
32. [User Roles & Capabilities](#user-roles--capabilities)
33. [Shortcodes Development](#shortcodes-development)
34. [Classic Widget Development](#classic-widget-development)
35. [theme.json Block Theme Configuration](#themejson-block-theme-configuration)
36. [WP-CLI Development](#wp-cli-development)

---

## Core Development Philosophy

### Prime Directives

1. **Human-Quality Code**: Write code that reads naturally, follows consistent patterns, and demonstrates deep WordPress expertise
2. **Security First**: Never trust user input, always sanitize, escape, and validate
3. **Performance Conscious**: Optimize queries, minimize HTTP requests, use caching appropriately
4. **Accessibility Compliant**: Follow WCAG 2.1 AA standards minimum
5. **Future-Proof**: Write extensible, hook-rich code that other developers can build upon
6. **Self-Documenting**: Code should be clear enough to understand without excessive comments

### Code Quality Markers

```php
// ✅ TOP 1% DEVELOPER CODE CHARACTERISTICS:
// - Consistent naming conventions throughout
// - Proper WordPress hook usage with correct priorities
// - Comprehensive error handling
// - Efficient database queries with proper caching
// - Full internationalization support
// - Extensive use of WordPress APIs over custom solutions
// - Clean separation of concerns (MVC-like patterns)
// - Proper use of namespaces and autoloading
// - PHPDoc blocks for all functions/methods
// - Graceful degradation and progressive enhancement
```

### Writing Human-Like Code (Avoiding AI-Generated Patterns)

To ensure code looks like it was written by an experienced human developer:

```php
// ❌ AVOID: Over-engineered, robotic naming
function perform_advanced_order_status_synchronization_with_external_service() {}
class AbstractBaseOrderProcessorFactoryManager {}

// ✅ PREFER: Natural, concise naming like a senior developer
function sync_order_status() {}
class Order_Sync_Manager {}

// ❌ AVOID: Generic, obvious comments
/**
 * This function gets the user data.
 * It retrieves user information from the database.
 * Returns an array of user data.
 */
function get_user_data( $user_id ) {}

// ✅ PREFER: Comments that explain "why", not "what"
/**
 * Get user data with meta fields needed for checkout validation.
 *
 * @param int $user_id User ID.
 * @return array User data including billing preferences.
 */
function prefix_get_user_checkout_data( int $user_id ): array {}

// ❌ AVOID: Over-abstraction and unnecessary layers
interface DataProviderInterface {}
abstract class AbstractDataProvider implements DataProviderInterface {}
class ConcreteUserDataProvider extends AbstractDataProvider {}
class UserDataProviderFactory {}

// ✅ PREFER: Pragmatic, hook-based WordPress architecture
class Prefix_User_Data {
    public function get( int $user_id ): array {
        return apply_filters( 'prefix_user_data', get_userdata( $user_id ), $user_id );
    }
}
```

**Key Principles for Human-Like Code:**

1. **Don't add comments about AI** - Never mention AI generation in code or comments
2. **Avoid generic comments** - Don't restate what the code obviously does
3. **Use natural naming** - Names should be concise and descriptive, like a human would write
4. **Don't over-abstract** - Avoid unnecessary interfaces, factories, and layers
5. **Follow WordPress patterns** - Use hook-based architecture, not enterprise Java patterns
6. **Keep it pragmatic** - If a solution looks strange or robotic, simplify it
7. **Favor incremental improvements** - When refactoring, improve existing code rather than rewriting from scratch

### Collaboration & Response Guidelines

When providing code assistance:

1. **Be Concrete**: Give actual implementation code, not pseudo-code. If something depends on a hook, option, or API, name it explicitly.

2. **Prefer Official Patterns**: Follow patterns from WordPress Developer Resources, WooCommerce docs, Elementor docs, and Crocoblock documentation.

3. **Explain Briefly**: After code, add 1-3 lines explaining:
   - What was done
   - Why it follows WordPress/WooCommerce standards

4. **Ask Only When Needed**: If enough information is provided, don't spam clarifying questions. For ambiguous architecture decisions:
   - State assumptions in a short note, OR
   - Ask one focused follow-up question

5. **Favor Incremental Improvements**: Prefer refactoring and improving existing code over rewriting from scratch (unless the design is clearly broken).

6. **Never Invent APIs**: Do not create fake WordPress/WooCommerce functions, hooks, or classes. Use only APIs that actually exist, or clearly mark placeholders as such.

---

## Error Handling, Logging & Debugging

> **Reference**: https://developer.wordpress.org/plugins/security/

### Error Handling Best Practices

```php
<?php
/**
 * Error handling patterns.
 *
 * @package Prefix_Plugin
 */

/**
 * Handle errors gracefully without exposing details to users.
 *
 * @param string $error_message Internal error message.
 * @param array  $context       Error context data.
 * @return void
 */
function prefix_handle_error( string $error_message, array $context = array() ) {
    // Never expose raw error messages on front-end.
    if ( ! is_admin() ) {
        // Show generic message to users.
        wp_die(
            esc_html__( 'Something went wrong. Please try again later.', 'textdomain' ),
            esc_html__( 'Error', 'textdomain' ),
            array( 'response' => 500 )
        );
    }
    
    // Log the actual error for debugging.
    prefix_log_error( $error_message, $context );
}

/**
 * Log errors using appropriate methods.
 *
 * @param string $message Error message.
 * @param array  $context Additional context.
 * @param string $level   Log level (debug, info, notice, warning, error, critical).
 * @return void
 */
function prefix_log_error( string $message, array $context = array(), string $level = 'error' ) {
    // Basic WordPress error logging.
    if ( defined( 'WP_DEBUG' ) && WP_DEBUG ) {
        if ( defined( 'WP_DEBUG_LOG' ) && WP_DEBUG_LOG ) {
            error_log( sprintf(
                '[Prefix Plugin] [%s] %s | Context: %s',
                strtoupper( $level ),
                $message,
                wp_json_encode( $context )
            ) );
        }
    }
}

/**
 * WooCommerce-specific logging.
 *
 * @param string $message Log message.
 * @param array  $context Additional context.
 * @param string $level   Log level.
 * @return void
 */
function prefix_wc_log( string $message, array $context = array(), string $level = 'info' ) {
    if ( ! function_exists( 'wc_get_logger' ) ) {
        return;
    }
    
    $logger = wc_get_logger();
    $logger->log( $level, $message, array_merge(
        array( 'source' => 'prefix-plugin' ),
        $context
    ) );
}

/**
 * Safe remote API call with error handling.
 *
 * @param string $url     API endpoint URL.
 * @param array  $args    Request arguments.
 * @return array|WP_Error Response data or error.
 */
function prefix_safe_api_call( string $url, array $args = array() ) {
    try {
        $response = wp_remote_get( $url, $args );
        
        if ( is_wp_error( $response ) ) {
            prefix_log_error( 'API call failed', array(
                'url'   => $url,
                'error' => $response->get_error_message(),
            ) );
            return $response;
        }
        
        $code = wp_remote_retrieve_response_code( $response );
        
        if ( $code < 200 || $code >= 300 ) {
            prefix_log_error( 'API returned non-success status', array(
                'url'    => $url,
                'status' => $code,
                'body'   => wp_remote_retrieve_body( $response ),
            ) );
            return new WP_Error(
                'api_error',
                sprintf( 'API returned status %d', $code ),
                array( 'status' => $code )
            );
        }
        
        $body = json_decode( wp_remote_retrieve_body( $response ), true );
        
        if ( json_last_error() !== JSON_ERROR_NONE ) {
            prefix_log_error( 'Failed to parse API response', array(
                'url'        => $url,
                'json_error' => json_last_error_msg(),
            ) );
            return new WP_Error( 'json_error', 'Invalid JSON response' );
        }
        
        return $body;
        
    } catch ( Exception $e ) {
        prefix_log_error( 'Exception during API call', array(
            'url'       => $url,
            'exception' => $e->getMessage(),
            'trace'     => $e->getTraceAsString(),
        ) );
        return new WP_Error( 'exception', $e->getMessage() );
    }
}

// WordPress Debug Constants Reference:
// WP_DEBUG        - Enable debug mode
// WP_DEBUG_LOG    - Log errors to wp-content/debug.log
// WP_DEBUG_DISPLAY - Display errors on screen (disable on production!)
// SCRIPT_DEBUG    - Use non-minified scripts
// SAVEQUERIES     - Save database queries for analysis
```

### Debugging Helpers

```php
<?php
/**
 * Debug helper functions (only active when WP_DEBUG is true).
 */

/**
 * Debug dump variable (only in debug mode).
 *
 * @param mixed  $var   Variable to dump.
 * @param string $label Optional label.
 * @return void
 */
function prefix_debug( $var, string $label = '' ) {
    if ( ! defined( 'WP_DEBUG' ) || ! WP_DEBUG ) {
        return;
    }
    
    $output = $label ? "[$label] " : '';
    $output .= print_r( $var, true ); // phpcs:ignore WordPress.PHP.DevelopmentFunctions.error_log_print_r
    
    error_log( $output ); // phpcs:ignore WordPress.PHP.DevelopmentFunctions.error_log_error_log
}

/**
 * Time a function execution (for performance debugging).
 *
 * @param callable $callback Function to time.
 * @param string   $label    Label for logging.
 * @return mixed Function result.
 */
function prefix_time_function( callable $callback, string $label = 'Function' ) {
    if ( ! defined( 'WP_DEBUG' ) || ! WP_DEBUG ) {
        return $callback();
    }
    
    $start = microtime( true );
    $result = $callback();
    $end = microtime( true );
    
    error_log( sprintf(
        '[Prefix Plugin] %s executed in %.4f seconds',
        $label,
        $end - $start
    ) );
    
    return $result;
}
```

---

## Data Privacy & Admin UX

### Data Collection Principles

```php
<?php
/**
 * Data privacy and admin UX guidelines.
 *
 * @package Prefix_Plugin
 */

// ✅ GOOD: Collect only required data
function prefix_save_user_preference( int $user_id, string $preference ) {
    // Only store what's necessary for the feature.
    update_user_meta( $user_id, '_prefix_display_preference', sanitize_key( $preference ) );
}

// ❌ BAD: Collecting unnecessary data
function prefix_save_user_preference_bad( int $user_id, string $preference ) {
    // Don't collect extra data "just in case".
    update_user_meta( $user_id, '_prefix_preference', $preference );
    update_user_meta( $user_id, '_prefix_ip_address', $_SERVER['REMOTE_ADDR'] ); // Unnecessary!
    update_user_meta( $user_id, '_prefix_browser', $_SERVER['HTTP_USER_AGENT'] ); // Unnecessary!
}
```

### Privacy Policy Integration

```php
<?php
/**
 * Register privacy policy content.
 *
 * @return void
 */
function prefix_add_privacy_policy_content() {
    if ( ! function_exists( 'wp_add_privacy_policy_content' ) ) {
        return;
    }
    
    $content = sprintf(
        '<h2>%s</h2><p>%s</p>',
        esc_html__( 'Prefix Plugin', 'textdomain' ),
        esc_html__( 'This plugin stores the following data: [describe what data is stored and why]. Data is retained for [time period] and can be exported/deleted via WordPress privacy tools.', 'textdomain' )
    );
    
    wp_add_privacy_policy_content( 'Prefix Plugin', wp_kses_post( $content ) );
}
add_action( 'admin_init', 'prefix_add_privacy_policy_content' );

/**
 * Register data exporter for privacy requests.
 *
 * @param array $exporters Existing exporters.
 * @return array Modified exporters.
 */
function prefix_register_data_exporter( array $exporters ): array {
    $exporters['prefix-plugin'] = array(
        'exporter_friendly_name' => __( 'Prefix Plugin Data', 'textdomain' ),
        'callback'               => 'prefix_data_exporter',
    );
    return $exporters;
}
add_filter( 'wp_privacy_personal_data_exporters', 'prefix_register_data_exporter' );

/**
 * Export user data for privacy request.
 *
 * @param string $email_address User email.
 * @param int    $page          Page number.
 * @return array Export data.
 */
function prefix_data_exporter( string $email_address, int $page = 1 ): array {
    $user = get_user_by( 'email', $email_address );
    $export_items = array();
    
    if ( $user ) {
        $preference = get_user_meta( $user->ID, '_prefix_display_preference', true );
        
        if ( $preference ) {
            $export_items[] = array(
                'group_id'    => 'prefix-plugin',
                'group_label' => __( 'Prefix Plugin Settings', 'textdomain' ),
                'item_id'     => 'user-preferences-' . $user->ID,
                'data'        => array(
                    array(
                        'name'  => __( 'Display Preference', 'textdomain' ),
                        'value' => $preference,
                    ),
                ),
            );
        }
    }
    
    return array(
        'data' => $export_items,
        'done' => true,
    );
}
```

### Admin UX Best Practices

```php
<?php
/**
 * Admin notices - do them right.
 */

// ✅ GOOD: Dismissible, targeted, non-intrusive notice
function prefix_admin_notice_setup() {
    // Only show on relevant pages.
    $screen = get_current_screen();
    if ( ! $screen || 'plugins' !== $screen->id ) {
        return;
    }
    
    // Check if already dismissed.
    if ( get_option( 'prefix_setup_notice_dismissed' ) ) {
        return;
    }
    
    // Check if setup is actually needed.
    if ( get_option( 'prefix_api_key' ) ) {
        return;
    }
    ?>
    <div class="notice notice-info is-dismissible" data-notice="prefix-setup">
        <p>
            <?php
            printf(
                /* translators: %s: Settings page URL */
                esc_html__( 'Prefix Plugin requires configuration. %s', 'textdomain' ),
                '<a href="' . esc_url( admin_url( 'admin.php?page=prefix-settings' ) ) . '">' . 
                esc_html__( 'Configure now', 'textdomain' ) . '</a>'
            );
            ?>
        </p>
    </div>
    <?php
}
add_action( 'admin_notices', 'prefix_admin_notice_setup' );

// ❌ BAD: Aggressive, non-dismissible, everywhere notice
function prefix_bad_admin_notice() {
    // Don't do this - shows on every admin page, not dismissible, promotional
    ?>
    <div class="notice notice-warning">
        <p>
            <strong>🚀 UPGRADE TO PRO NOW! 🚀</strong>
            Get 50% off our premium version! Limited time only!
            <a href="#">BUY NOW!</a>
        </p>
    </div>
    <?php
}

/**
 * Handle notice dismissal via AJAX.
 *
 * @return void
 */
function prefix_dismiss_admin_notice() {
    check_ajax_referer( 'prefix_dismiss_notice', 'nonce' );
    
    if ( ! current_user_can( 'manage_options' ) ) {
        wp_send_json_error( 'Permission denied' );
    }
    
    $notice = isset( $_POST['notice'] ) ? sanitize_key( $_POST['notice'] ) : '';
    
    if ( 'prefix-setup' === $notice ) {
        update_option( 'prefix_setup_notice_dismissed', true );
    }
    
    wp_send_json_success();
}
add_action( 'wp_ajax_prefix_dismiss_notice', 'prefix_dismiss_admin_notice' );
```

### External Calls & Tracking Opt-In

```php
<?php
/**
 * If your plugin makes external calls or tracks usage, require opt-in.
 */

/**
 * Check if user has opted in to usage tracking.
 *
 * @return bool Whether tracking is enabled.
 */
function prefix_is_tracking_enabled(): bool {
    return 'yes' === get_option( 'prefix_allow_tracking', 'no' );
}

/**
 * Tracking opt-in setting.
 */
function prefix_tracking_setting() {
    add_settings_field(
        'prefix_allow_tracking',
        __( 'Usage Tracking', 'textdomain' ),
        'prefix_tracking_field_callback',
        'prefix-settings',
        'prefix_general_section'
    );
}

function prefix_tracking_field_callback() {
    $value = get_option( 'prefix_allow_tracking', 'no' );
    ?>
    <label>
        <input type="checkbox" name="prefix_allow_tracking" value="yes" <?php checked( $value, 'yes' ); ?>>
        <?php esc_html_e( 'Help improve this plugin by sending anonymous usage data', 'textdomain' ); ?>
    </label>
    <p class="description">
        <?php esc_html_e( 'We collect: plugin version, WordPress version, PHP version. We never collect personal data or site content.', 'textdomain' ); ?>
    </p>
    <?php
}
```

---

## Environment & Compatibility

### Version Requirements

```php
<?php
/**
 * Environment and compatibility checks.
 *
 * @package Prefix_Plugin
 */

// Recommended minimums (unless project specifies otherwise):
// - PHP 7.4+ (or 8.0+ for new projects)
// - WordPress 6.0+
// - WooCommerce 7.0+ (if WooCommerce is required)

/**
 * Check environment requirements.
 *
 * @return bool|WP_Error True if requirements met, WP_Error otherwise.
 */
function prefix_check_environment() {
    $errors = array();
    
    // PHP version check.
    if ( version_compare( PHP_VERSION, '7.4', '<' ) ) {
        $errors[] = sprintf(
            /* translators: 1: Required PHP version, 2: Current PHP version */
            __( 'PHP %1$s or higher is required. You are running PHP %2$s.', 'textdomain' ),
            '7.4',
            PHP_VERSION
        );
    }
    
    // WordPress version check.
    global $wp_version;
    if ( version_compare( $wp_version, '6.0', '<' ) ) {
        $errors[] = sprintf(
            /* translators: 1: Required WP version, 2: Current WP version */
            __( 'WordPress %1$s or higher is required. You are running WordPress %2$s.', 'textdomain' ),
            '6.0',
            $wp_version
        );
    }
    
    // WooCommerce check (if required).
    if ( defined( 'PREFIX_REQUIRES_WOOCOMMERCE' ) && PREFIX_REQUIRES_WOOCOMMERCE ) {
        if ( ! class_exists( 'WooCommerce' ) ) {
            $errors[] = __( 'WooCommerce must be installed and activated.', 'textdomain' );
        } elseif ( defined( 'WC_VERSION' ) && version_compare( WC_VERSION, '7.0', '<' ) ) {
            $errors[] = sprintf(
                /* translators: 1: Required WC version, 2: Current WC version */
                __( 'WooCommerce %1$s or higher is required. You are running WooCommerce %2$s.', 'textdomain' ),
                '7.0',
                WC_VERSION
            );
        }
    }
    
    if ( ! empty( $errors ) ) {
        return new WP_Error( 'requirements_not_met', implode( ' ', $errors ) );
    }
    
    return true;
}
```

### Handling Deprecated Functions

```php
<?php
/**
 * Handling deprecated WordPress/WooCommerce functions.
 */

// Example: wc_get_order() is preferred over new WC_Order() since WC 2.2

// ❌ DEPRECATED: Direct instantiation
$order = new WC_Order( $order_id );

// ✅ CURRENT: Use factory function
$order = wc_get_order( $order_id );

// Example: Handling a function that might not exist in older versions
if ( function_exists( 'wp_get_environment_type' ) ) {
    $env = wp_get_environment_type();
} else {
    // Fallback for WordPress < 5.5
    $env = defined( 'WP_ENVIRONMENT_TYPE' ) ? WP_ENVIRONMENT_TYPE : 'production';
}

/**
 * Wrapper for potentially deprecated function.
 *
 * @param int $order_id Order ID.
 * @return WC_Order|false Order object or false.
 */
function prefix_get_order( int $order_id ) {
    // Always use the current recommended method.
    return wc_get_order( $order_id );
}

/**
 * Check if we're using HPOS (High-Performance Order Storage).
 *
 * @return bool Whether HPOS is enabled.
 */
function prefix_is_hpos_enabled(): bool {
    if ( ! class_exists( 'Automattic\WooCommerce\Utilities\OrderUtil' ) ) {
        return false;
    }
    return Automattic\WooCommerce\Utilities\OrderUtil::custom_orders_table_usage_is_enabled();
}
```

### Scalability Considerations

```php
<?php
/**
 * Design with scale in mind - thousands of posts/orders/products.
 */

// ❌ BAD: Will timeout with large datasets
function prefix_get_all_orders_bad() {
    $orders = wc_get_orders( array(
        'limit' => -1, // Gets ALL orders - dangerous!
    ) );
    
    foreach ( $orders as $order ) {
        // Process each order...
    }
}

// ✅ GOOD: Batch processing with pagination
function prefix_process_orders_batch( int $batch_size = 100 ) {
    $page = 1;
    
    do {
        $orders = wc_get_orders( array(
            'limit'  => $batch_size,
            'page'   => $page,
            'status' => array( 'processing', 'completed' ),
        ) );
        
        foreach ( $orders as $order ) {
            prefix_process_single_order( $order );
        }
        
        $page++;
        
        // Prevent timeout on large sites.
        if ( function_exists( 'wp_cache_flush' ) ) {
            wp_cache_flush();
        }
        
    } while ( count( $orders ) === $batch_size );
}

// ✅ GOOD: Use background processing for heavy operations
function prefix_schedule_batch_processing() {
    if ( ! wp_next_scheduled( 'prefix_batch_process' ) ) {
        wp_schedule_single_event( time(), 'prefix_batch_process' );
    }
}

// ✅ GOOD: Cache expensive queries
function prefix_get_product_count_by_category( int $category_id ): int {
    $cache_key = 'prefix_product_count_' . $category_id;
    $count = get_transient( $cache_key );
    
    if ( false === $count ) {
        $count = count( wc_get_products( array(
            'category' => array( $category_id ),
            'return'   => 'ids',
            'limit'    => -1,
        ) ) );
        
        set_transient( $cache_key, $count, HOUR_IN_SECONDS );
    }
    
    return (int) $count;
}
```

---

## WordPress PHP Coding Standards

> **Reference**: https://developer.wordpress.org/coding-standards/wordpress-coding-standards/php/

### Naming Conventions

```php
// Functions: lowercase with underscores, prefixed
function prefix_get_user_data( $user_id ) {}
function prefix_process_order_items( $order ) {}

// Classes: Capitalized words separated by underscores
class Prefix_User_Handler {}
class Prefix_WC_Order_Processor {}

// Interfaces, Traits, Enums
interface Prefix_Data_Interface {}
trait Prefix_Singleton_Trait {}
enum Prefix_Status_Enum {}

// Constants: ALL CAPS with underscores
define( 'PREFIX_PLUGIN_VERSION', '1.0.0' );
const PREFIX_MAX_ITEMS = 100;

// Files: lowercase with hyphens
// class-prefix-user-handler.php
// interface-prefix-data.php

// Variables: lowercase with underscores (never camelCase)
$user_data = array();
$order_total = 0;
$is_active = true;
```

### Spacing and Formatting

```php
<?php
/**
 * Always use full PHP tags, never shorthand
 */

// Spaces inside parentheses for control structures
if ( $condition ) {
    // code
}

foreach ( $items as $item ) {
    // code
}

while ( $condition ) {
    // code
}

switch ( $value ) {
    case 'option':
        // code
        break;
    default:
        // code
        break;
}

// No spaces for function calls
$result = my_function( $arg1, $arg2 );
$value = absint( $input );

// Spaces around operators
$sum = $a + $b;
$result = $value === true;
$concat = $string1 . $string2;

// Array syntax - use array() for PHP 5.6 compat, or [] for PHP 7.0+
$array = array(
    'key1' => 'value1',
    'key2' => 'value2',
);

// Short array syntax (PHP 7.0+)
$array = [
    'key1' => 'value1',
    'key2' => 'value2',
];

// Array item access - space only for variables
$value = $array['key'];
$value = $array[ $variable_key ];
```

### Yoda Conditions

```php
// ✅ CORRECT - Yoda conditions prevent accidental assignment
if ( true === $value ) {}
if ( 'string' === $type ) {}
if ( null === $result ) {}
if ( 0 === $count ) {}

// ❌ INCORRECT
if ( $value === true ) {}
if ( $type === 'string' ) {}
```

### Type Declarations (PHP 7.0+)

```php
/**
 * Process user data with strict typing.
 *
 * @param int    $user_id User ID.
 * @param string $action  Action to perform.
 * @param array  $data    Additional data.
 * @return bool Whether the operation was successful.
 */
function prefix_process_user( int $user_id, string $action, array $data = array() ): bool {
    // Implementation
    return true;
}

// Class with typed properties (PHP 7.4+)
class Prefix_User {
    private int $id;
    private string $name;
    private ?string $email = null;
    private array $meta = [];
    
    public function __construct( int $id, string $name ) {
        $this->id = $id;
        $this->name = $name;
    }
}
```

### Brace Style

```php
// Opening brace on same line
if ( $condition ) {
    // code
} elseif ( $other_condition ) {
    // code
} else {
    // code
}

// Functions and classes
function prefix_my_function() {
    // code
}

class Prefix_My_Class {
    public function my_method() {
        // code
    }
}

// Always use braces, even for single statements
if ( $condition ) {
    return true;
}

// ❌ NEVER do this
if ( $condition ) return true;
```

### String Handling

```php
// Single quotes for simple strings
$name = 'John';

// Double quotes when variables are needed
$message = "Hello, {$name}!";

// Prefer sprintf for complex strings
$output = sprintf(
    /* translators: 1: User name, 2: Date */
    __( 'Welcome %1$s! Your account was created on %2$s.', 'textdomain' ),
    esc_html( $user_name ),
    esc_html( $date )
);

// Heredoc for multiline HTML
$html = <<<HTML
<div class="wrapper">
    <h2>{$escaped_title}</h2>
    <p>{$escaped_content}</p>
</div>
HTML;
```

---

## WordPress JavaScript Coding Standards

> **Reference**: https://developer.wordpress.org/coding-standards/wordpress-coding-standards/javascript/

### General Formatting

```javascript
/**
 * WordPress JavaScript follows jQuery style guide with modifications.
 */

// Use tabs for indentation
// Use single quotes for strings
// Always use strict equality
// Declare variables at top of scope

( function( $ ) {
    'use strict';
    
    // Variables declared at top
    var $container,
        currentIndex = 0,
        items = [],
        isLoading = false;
    
    /**
     * Initialize the module.
     *
     * @return {void}
     */
    function init() {
        $container = $( '.prefix-container' );
        bindEvents();
    }
    
    /**
     * Bind event handlers.
     *
     * @return {void}
     */
    function bindEvents() {
        $container.on( 'click', '.prefix-button', handleButtonClick );
        $( document ).on( 'prefix:custom-event', handleCustomEvent );
    }
    
    /**
     * Handle button click.
     *
     * @param {Event} event Click event.
     * @return {void}
     */
    function handleButtonClick( event ) {
        event.preventDefault();
        
        var $button = $( this ),
            itemId = $button.data( 'item-id' );
        
        if ( ! itemId ) {
            return;
        }
        
        processItem( itemId );
    }
    
    /**
     * Process an item via AJAX.
     *
     * @param {number} itemId Item ID to process.
     * @return {void}
     */
    function processItem( itemId ) {
        if ( isLoading ) {
            return;
        }
        
        isLoading = true;
        
        $.ajax( {
            url: prefixSettings.ajaxUrl,
            type: 'POST',
            data: {
                action: 'prefix_process_item',
                item_id: itemId,
                nonce: prefixSettings.nonce
            },
            success: function( response ) {
                if ( response.success ) {
                    updateUI( response.data );
                } else {
                    showError( response.data.message );
                }
            },
            error: function( xhr, status, error ) {
                showError( 'An error occurred. Please try again.' );
                console.error( 'AJAX Error:', status, error );
            },
            complete: function() {
                isLoading = false;
            }
        } );
    }
    
    // Initialize on document ready
    $( document ).ready( init );
    
} )( jQuery );
```

### Modern ES6+ JavaScript (for Block Editor/React)

```javascript
/**
 * Modern JavaScript for Gutenberg blocks.
 */
import { __ } from '@wordpress/i18n';
import { registerBlockType } from '@wordpress/blocks';
import { useBlockProps, RichText, InspectorControls } from '@wordpress/block-editor';
import { PanelBody, TextControl, ToggleControl } from '@wordpress/components';
import { useState, useEffect } from '@wordpress/element';

/**
 * Register custom block.
 */
registerBlockType( 'prefix/custom-block', {
    title: __( 'Custom Block', 'textdomain' ),
    description: __( 'A custom block for demonstration.', 'textdomain' ),
    category: 'widgets',
    icon: 'admin-generic',
    keywords: [
        __( 'custom', 'textdomain' ),
        __( 'block', 'textdomain' ),
    ],
    attributes: {
        title: {
            type: 'string',
            default: '',
        },
        content: {
            type: 'string',
            default: '',
        },
        showBorder: {
            type: 'boolean',
            default: false,
        },
    },
    
    /**
     * Edit component.
     *
     * @param {Object} props Block props.
     * @return {WPElement} Element to render.
     */
    edit: ( { attributes, setAttributes } ) => {
        const { title, content, showBorder } = attributes;
        const [ isLoading, setIsLoading ] = useState( false );
        
        const blockProps = useBlockProps( {
            className: showBorder ? 'has-border' : '',
        } );
        
        useEffect( () => {
            // Component mount logic
            return () => {
                // Cleanup
            };
        }, [] );
        
        return (
            <>
                <InspectorControls>
                    <PanelBody title={ __( 'Settings', 'textdomain' ) }>
                        <ToggleControl
                            label={ __( 'Show Border', 'textdomain' ) }
                            checked={ showBorder }
                            onChange={ ( value ) => setAttributes( { showBorder: value } ) }
                        />
                    </PanelBody>
                </InspectorControls>
                
                <div { ...blockProps }>
                    <RichText
                        tagName="h2"
                        value={ title }
                        onChange={ ( value ) => setAttributes( { title: value } ) }
                        placeholder={ __( 'Enter title...', 'textdomain' ) }
                    />
                    <RichText
                        tagName="p"
                        value={ content }
                        onChange={ ( value ) => setAttributes( { content: value } ) }
                        placeholder={ __( 'Enter content...', 'textdomain' ) }
                    />
                </div>
            </>
        );
    },
    
    /**
     * Save component.
     *
     * @param {Object} props Block props.
     * @return {WPElement} Element to render.
     */
    save: ( { attributes } ) => {
        const { title, content, showBorder } = attributes;
        
        const blockProps = useBlockProps.save( {
            className: showBorder ? 'has-border' : '',
        } );
        
        return (
            <div { ...blockProps }>
                <RichText.Content tagName="h2" value={ title } />
                <RichText.Content tagName="p" value={ content } />
            </div>
        );
    },
} );
```

---

## WordPress CSS/SCSS Coding Standards

> **Reference**: https://developer.wordpress.org/coding-standards/wordpress-coding-standards/css/

### CSS Structure and Formatting

```css
/**
 * CSS follows WordPress standards with BEM-like naming.
 * 
 * Table of Contents:
 * 1. Base Styles
 * 2. Layout
 * 3. Components
 * 4. Utilities
 */

/* ==========================================================================
   1. Base Styles
   ========================================================================== */

/**
 * Root variables for theming.
 */
:root {
    --prefix-primary-color: #0073aa;
    --prefix-secondary-color: #23282d;
    --prefix-text-color: #333333;
    --prefix-border-radius: 4px;
    --prefix-spacing-unit: 8px;
    --prefix-transition-speed: 0.3s;
}

/* ==========================================================================
   2. Layout
   ========================================================================== */

/**
 * Container styles.
 */
.prefix-container {
    display: flex;
    flex-wrap: wrap;
    max-width: 1200px;
    margin-right: auto;
    margin-left: auto;
    padding-right: calc(var(--prefix-spacing-unit) * 2);
    padding-left: calc(var(--prefix-spacing-unit) * 2);
}

/* ==========================================================================
   3. Components
   ========================================================================== */

/**
 * Card component.
 */
.prefix-card {
    display: flex;
    flex-direction: column;
    background-color: #ffffff;
    border: 1px solid #dddddd;
    border-radius: var(--prefix-border-radius);
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    transition: box-shadow var(--prefix-transition-speed) ease;
}

.prefix-card:hover {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

.prefix-card__header {
    padding: calc(var(--prefix-spacing-unit) * 2);
    border-bottom: 1px solid #eeeeee;
}

.prefix-card__title {
    margin: 0;
    font-size: 1.25rem;
    font-weight: 600;
    line-height: 1.4;
    color: var(--prefix-text-color);
}

.prefix-card__body {
    flex: 1;
    padding: calc(var(--prefix-spacing-unit) * 2);
}

.prefix-card__footer {
    display: flex;
    justify-content: flex-end;
    gap: var(--prefix-spacing-unit);
    padding: calc(var(--prefix-spacing-unit) * 2);
    border-top: 1px solid #eeeeee;
}

/**
 * Button component.
 */
.prefix-button {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    min-height: 36px;
    padding: calc(var(--prefix-spacing-unit) * 0.5) calc(var(--prefix-spacing-unit) * 2);
    font-size: 14px;
    font-weight: 500;
    line-height: 1.4;
    color: #ffffff;
    text-decoration: none;
    cursor: pointer;
    background-color: var(--prefix-primary-color);
    border: 1px solid transparent;
    border-radius: var(--prefix-border-radius);
    transition: background-color var(--prefix-transition-speed) ease,
                border-color var(--prefix-transition-speed) ease;
}

.prefix-button:hover,
.prefix-button:focus {
    color: #ffffff;
    text-decoration: none;
    background-color: #005a87;
}

.prefix-button:focus {
    outline: 2px solid var(--prefix-primary-color);
    outline-offset: 2px;
}

.prefix-button--secondary {
    color: var(--prefix-text-color);
    background-color: transparent;
    border-color: #dddddd;
}

.prefix-button--secondary:hover,
.prefix-button--secondary:focus {
    color: var(--prefix-primary-color);
    background-color: #f7f7f7;
    border-color: var(--prefix-primary-color);
}

/* ==========================================================================
   4. Utilities
   ========================================================================== */

/**
 * Screen reader text.
 */
.prefix-screen-reader-text {
    position: absolute !important;
    width: 1px;
    height: 1px;
    margin: -1px;
    padding: 0;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    word-wrap: normal !important;
    border: 0;
}

/**
 * Clearfix.
 */
.prefix-clearfix::after {
    display: table;
    clear: both;
    content: "";
}

/* ==========================================================================
   5. Responsive
   ========================================================================== */

/**
 * Mobile first responsive design.
 */
@media screen and (min-width: 782px) {
    .prefix-container {
        padding-right: calc(var(--prefix-spacing-unit) * 3);
        padding-left: calc(var(--prefix-spacing-unit) * 3);
    }
}

@media screen and (min-width: 1200px) {
    .prefix-container {
        padding-right: calc(var(--prefix-spacing-unit) * 4);
        padding-left: calc(var(--prefix-spacing-unit) * 4);
    }
}
```

### SCSS Standards

```scss
/**
 * SCSS file structure with WordPress standards.
 */

// ==========================================================================
// Variables
// ==========================================================================

$prefix-primary-color: #0073aa;
$prefix-secondary-color: #23282d;
$prefix-success-color: #46b450;
$prefix-warning-color: #ffb900;
$prefix-error-color: #dc3232;

$prefix-font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
$prefix-font-size-base: 14px;
$prefix-line-height-base: 1.5;

$prefix-spacing-xs: 4px;
$prefix-spacing-sm: 8px;
$prefix-spacing-md: 16px;
$prefix-spacing-lg: 24px;
$prefix-spacing-xl: 32px;

$prefix-border-radius: 4px;
$prefix-transition-speed: 0.3s;

// Breakpoints
$prefix-breakpoint-sm: 600px;
$prefix-breakpoint-md: 782px;
$prefix-breakpoint-lg: 1024px;
$prefix-breakpoint-xl: 1200px;

// ==========================================================================
// Mixins
// ==========================================================================

@mixin prefix-respond-to($breakpoint) {
    @if $breakpoint == sm {
        @media screen and (min-width: $prefix-breakpoint-sm) { @content; }
    } @else if $breakpoint == md {
        @media screen and (min-width: $prefix-breakpoint-md) { @content; }
    } @else if $breakpoint == lg {
        @media screen and (min-width: $prefix-breakpoint-lg) { @content; }
    } @else if $breakpoint == xl {
        @media screen and (min-width: $prefix-breakpoint-xl) { @content; }
    }
}

@mixin prefix-button-base {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    min-height: 36px;
    padding: $prefix-spacing-xs $prefix-spacing-md;
    font-family: $prefix-font-family;
    font-size: $prefix-font-size-base;
    font-weight: 500;
    line-height: $prefix-line-height-base;
    text-decoration: none;
    cursor: pointer;
    border-radius: $prefix-border-radius;
    transition: background-color $prefix-transition-speed ease,
                border-color $prefix-transition-speed ease,
                color $prefix-transition-speed ease;
    
    &:focus {
        outline: 2px solid $prefix-primary-color;
        outline-offset: 2px;
    }
}

@mixin prefix-card {
    background-color: #ffffff;
    border: 1px solid #dddddd;
    border-radius: $prefix-border-radius;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

// ==========================================================================
// Components
// ==========================================================================

.prefix-button {
    @include prefix-button-base;
    color: #ffffff;
    background-color: $prefix-primary-color;
    border: 1px solid transparent;
    
    &:hover,
    &:focus {
        color: #ffffff;
        background-color: darken($prefix-primary-color, 10%);
    }
    
    &--secondary {
        color: $prefix-secondary-color;
        background-color: transparent;
        border-color: #dddddd;
        
        &:hover,
        &:focus {
            color: $prefix-primary-color;
            background-color: #f7f7f7;
            border-color: $prefix-primary-color;
        }
    }
    
    &--small {
        min-height: 28px;
        padding: 2px $prefix-spacing-sm;
        font-size: 12px;
    }
    
    &--large {
        min-height: 44px;
        padding: $prefix-spacing-sm $prefix-spacing-lg;
        font-size: 16px;
    }
}

.prefix-card {
    @include prefix-card;
    
    &__header {
        padding: $prefix-spacing-md;
        border-bottom: 1px solid #eeeeee;
    }
    
    &__title {
        margin: 0;
        font-size: 1.25rem;
        font-weight: 600;
    }
    
    &__body {
        padding: $prefix-spacing-md;
    }
    
    &__footer {
        display: flex;
        justify-content: flex-end;
        gap: $prefix-spacing-sm;
        padding: $prefix-spacing-md;
        border-top: 1px solid #eeeeee;
    }
}
```

---

## WordPress HTML Coding Standards

> **Reference**: https://developer.wordpress.org/coding-standards/wordpress-coding-standards/html/

### HTML Best Practices

```html
<!-- Always use semantic HTML5 -->
<!DOCTYPE html>
<html <?php language_attributes(); ?>>
<head>
    <meta charset="<?php bloginfo( 'charset' ); ?>">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <?php wp_head(); ?>
</head>
<body <?php body_class(); ?>>
<?php wp_body_open(); ?>

<header class="site-header" role="banner">
    <nav class="main-navigation" role="navigation" aria-label="<?php esc_attr_e( 'Primary Menu', 'textdomain' ); ?>">
        <!-- Navigation content -->
    </nav>
</header>

<main id="main-content" class="site-main" role="main">
    <article id="post-<?php the_ID(); ?>" <?php post_class(); ?>>
        <header class="entry-header">
            <h1 class="entry-title"><?php the_title(); ?></h1>
        </header>
        
        <div class="entry-content">
            <?php the_content(); ?>
        </div>
        
        <footer class="entry-footer">
            <!-- Post meta -->
        </footer>
    </article>
</main>

<aside class="sidebar" role="complementary" aria-label="<?php esc_attr_e( 'Sidebar', 'textdomain' ); ?>">
    <?php dynamic_sidebar( 'sidebar-1' ); ?>
</aside>

<footer class="site-footer" role="contentinfo">
    <!-- Footer content -->
</footer>

<?php wp_footer(); ?>
</body>
</html>
```

### Accessibility Requirements

```html
<!-- All images must have alt text -->
<img src="<?php echo esc_url( $image_url ); ?>" 
     alt="<?php echo esc_attr( $alt_text ); ?>"
     width="300"
     height="200"
     loading="lazy">

<!-- Form labels must be associated with inputs -->
<label for="prefix-email">
    <?php esc_html_e( 'Email Address', 'textdomain' ); ?>
    <span class="required" aria-hidden="true">*</span>
</label>
<input type="email" 
       id="prefix-email" 
       name="email" 
       required 
       aria-required="true"
       aria-describedby="prefix-email-description">
<p id="prefix-email-description" class="description">
    <?php esc_html_e( 'We will never share your email.', 'textdomain' ); ?>
</p>

<!-- Buttons must have accessible names -->
<button type="submit" class="prefix-button" aria-label="<?php esc_attr_e( 'Submit form', 'textdomain' ); ?>">
    <?php esc_html_e( 'Submit', 'textdomain' ); ?>
</button>

<!-- Interactive elements need focus states -->
<a href="<?php echo esc_url( $url ); ?>" 
   class="prefix-link"
   aria-label="<?php echo esc_attr( sprintf( __( 'Read more about %s', 'textdomain' ), $title ) ); ?>">
    <?php esc_html_e( 'Read More', 'textdomain' ); ?>
</a>

<!-- Skip links for keyboard navigation -->
<a href="#main-content" class="skip-link screen-reader-text">
    <?php esc_html_e( 'Skip to main content', 'textdomain' ); ?>
</a>

<!-- Tables must have proper structure -->
<table class="prefix-table">
    <caption class="screen-reader-text">
        <?php esc_html_e( 'Product comparison table', 'textdomain' ); ?>
    </caption>
    <thead>
        <tr>
            <th scope="col"><?php esc_html_e( 'Product', 'textdomain' ); ?></th>
            <th scope="col"><?php esc_html_e( 'Price', 'textdomain' ); ?></th>
            <th scope="col"><?php esc_html_e( 'Rating', 'textdomain' ); ?></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><?php echo esc_html( $product_name ); ?></td>
            <td><?php echo wp_kses_post( wc_price( $price ) ); ?></td>
            <td>
                <span aria-label="<?php echo esc_attr( sprintf( __( '%s out of 5 stars', 'textdomain' ), $rating ) ); ?>">
                    <?php echo esc_html( $rating ); ?>
                </span>
            </td>
        </tr>
    </tbody>
</table>
```

---

## Plugin Development Standards

> **Reference**: https://developer.wordpress.org/plugins/

### Main Plugin File Structure

```php
<?php
/**
 * Plugin Name:       Prefix Plugin Name
 * Plugin URI:        https://example.com/plugin-name
 * Description:       A brief description of the plugin functionality.
 * Version:           1.0.0
 * Requires at least: 5.8
 * Requires PHP:      7.4
 * Author:            Your Name
 * Author URI:        https://example.com
 * License:           GPL v2 or later
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain:       prefix-plugin-name
 * Domain Path:       /languages
 * Network:           false
 *
 * WC requires at least: 7.0
 * WC tested up to:      8.5
 *
 * @package Prefix_Plugin_Name
 */

// Exit if accessed directly.
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Plugin version.
 *
 * @var string
 */
define( 'PREFIX_PLUGIN_VERSION', '1.0.0' );

/**
 * Plugin directory path.
 *
 * @var string
 */
define( 'PREFIX_PLUGIN_DIR', plugin_dir_path( __FILE__ ) );

/**
 * Plugin directory URL.
 *
 * @var string
 */
define( 'PREFIX_PLUGIN_URL', plugin_dir_url( __FILE__ ) );

/**
 * Plugin basename.
 *
 * @var string
 */
define( 'PREFIX_PLUGIN_BASENAME', plugin_basename( __FILE__ ) );

/**
 * Minimum PHP version.
 *
 * @var string
 */
define( 'PREFIX_MINIMUM_PHP_VERSION', '7.4' );

/**
 * Minimum WordPress version.
 *
 * @var string
 */
define( 'PREFIX_MINIMUM_WP_VERSION', '5.8' );

/**
 * Check plugin requirements before loading.
 *
 * @return bool Whether requirements are met.
 */
function prefix_check_requirements() {
    $errors = array();
    
    // Check PHP version.
    if ( version_compare( PHP_VERSION, PREFIX_MINIMUM_PHP_VERSION, '<' ) ) {
        $errors[] = sprintf(
            /* translators: 1: Required PHP version, 2: Current PHP version */
            __( 'Prefix Plugin requires PHP version %1$s or higher. Your server is running PHP %2$s.', 'prefix-plugin-name' ),
            PREFIX_MINIMUM_PHP_VERSION,
            PHP_VERSION
        );
    }
    
    // Check WordPress version.
    if ( version_compare( get_bloginfo( 'version' ), PREFIX_MINIMUM_WP_VERSION, '<' ) ) {
        $errors[] = sprintf(
            /* translators: 1: Required WP version, 2: Current WP version */
            __( 'Prefix Plugin requires WordPress version %1$s or higher. You are running WordPress %2$s.', 'prefix-plugin-name' ),
            PREFIX_MINIMUM_WP_VERSION,
            get_bloginfo( 'version' )
        );
    }
    
    if ( ! empty( $errors ) ) {
        add_action( 'admin_notices', function() use ( $errors ) {
            ?>
            <div class="notice notice-error">
                <?php foreach ( $errors as $error ) : ?>
                    <p><?php echo esc_html( $error ); ?></p>
                <?php endforeach; ?>
            </div>
            <?php
        } );
        return false;
    }
    
    return true;
}

/**
 * Load plugin textdomain for translations.
 *
 * @return void
 */
function prefix_load_textdomain() {
    load_plugin_textdomain(
        'prefix-plugin-name',
        false,
        dirname( PREFIX_PLUGIN_BASENAME ) . '/languages'
    );
}
add_action( 'init', 'prefix_load_textdomain' );

/**
 * Initialize plugin.
 *
 * @return void
 */
function prefix_init() {
    if ( ! prefix_check_requirements() ) {
        return;
    }
    
    // Load autoloader.
    require_once PREFIX_PLUGIN_DIR . 'includes/class-prefix-autoloader.php';
    
    // Initialize main plugin class.
    Prefix_Plugin_Name::instance();
}
add_action( 'plugins_loaded', 'prefix_init' );

/**
 * Plugin activation hook.
 *
 * @return void
 */
function prefix_activate() {
    if ( ! prefix_check_requirements() ) {
        deactivate_plugins( PREFIX_PLUGIN_BASENAME );
        wp_die(
            esc_html__( 'Plugin activation failed. Please check your PHP and WordPress versions.', 'prefix-plugin-name' ),
            esc_html__( 'Plugin Activation Error', 'prefix-plugin-name' ),
            array( 'back_link' => true )
        );
    }
    
    // Create database tables.
    require_once PREFIX_PLUGIN_DIR . 'includes/class-prefix-installer.php';
    Prefix_Installer::install();
    
    // Set default options.
    add_option( 'prefix_plugin_version', PREFIX_PLUGIN_VERSION );
    add_option( 'prefix_plugin_settings', prefix_get_default_settings() );
    
    // Schedule cron events.
    if ( ! wp_next_scheduled( 'prefix_daily_cron' ) ) {
        wp_schedule_event( time(), 'daily', 'prefix_daily_cron' );
    }
    
    // Flush rewrite rules.
    flush_rewrite_rules();
}
register_activation_hook( __FILE__, 'prefix_activate' );

/**
 * Plugin deactivation hook.
 *
 * @return void
 */
function prefix_deactivate() {
    // Clear scheduled events.
    wp_clear_scheduled_hook( 'prefix_daily_cron' );
    
    // Flush rewrite rules.
    flush_rewrite_rules();
}
register_deactivation_hook( __FILE__, 'prefix_deactivate' );

/**
 * Get default plugin settings.
 *
 * @return array Default settings.
 */
function prefix_get_default_settings() {
    return apply_filters( 'prefix_default_settings', array(
        'enable_feature'  => true,
        'items_per_page'  => 10,
        'cache_duration'  => 3600,
        'debug_mode'      => false,
    ) );
}
```

### Plugin Class Structure

```php
<?php
/**
 * Main plugin class.
 *
 * @package Prefix_Plugin_Name
 */

// Exit if accessed directly.
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Main Plugin Class.
 *
 * @since 1.0.0
 */
final class Prefix_Plugin_Name {

    /**
     * Plugin version.
     *
     * @var string
     */
    public $version = PREFIX_PLUGIN_VERSION;

    /**
     * Single instance of the class.
     *
     * @var Prefix_Plugin_Name|null
     */
    private static $instance = null;

    /**
     * Admin instance.
     *
     * @var Prefix_Admin|null
     */
    public $admin = null;

    /**
     * Frontend instance.
     *
     * @var Prefix_Frontend|null
     */
    public $frontend = null;

    /**
     * AJAX handler instance.
     *
     * @var Prefix_Ajax|null
     */
    public $ajax = null;

    /**
     * Get single instance of the class.
     *
     * @return Prefix_Plugin_Name
     */
    public static function instance() {
        if ( is_null( self::$instance ) ) {
            self::$instance = new self();
        }
        return self::$instance;
    }

    /**
     * Constructor.
     */
    private function __construct() {
        $this->define_constants();
        $this->includes();
        $this->init_hooks();
        
        /**
         * Fires after plugin is fully loaded.
         *
         * @since 1.0.0
         * @param Prefix_Plugin_Name $this Main plugin instance.
         */
        do_action( 'prefix_plugin_loaded', $this );
    }

    /**
     * Prevent cloning.
     *
     * @return void
     */
    public function __clone() {
        _doing_it_wrong(
            __FUNCTION__,
            esc_html__( 'Cloning is forbidden.', 'prefix-plugin-name' ),
            '1.0.0'
        );
    }

    /**
     * Prevent unserializing.
     *
     * @return void
     */
    public function __wakeup() {
        _doing_it_wrong(
            __FUNCTION__,
            esc_html__( 'Unserializing is forbidden.', 'prefix-plugin-name' ),
            '1.0.0'
        );
    }

    /**
     * Define additional constants.
     *
     * @return void
     */
    private function define_constants() {
        $this->define( 'PREFIX_ABSPATH', dirname( PREFIX_PLUGIN_DIR ) . '/' );
        $this->define( 'PREFIX_INCLUDES_DIR', PREFIX_PLUGIN_DIR . 'includes/' );
        $this->define( 'PREFIX_TEMPLATES_DIR', PREFIX_PLUGIN_DIR . 'templates/' );
    }

    /**
     * Define constant if not already defined.
     *
     * @param string $name  Constant name.
     * @param mixed  $value Constant value.
     * @return void
     */
    private function define( $name, $value ) {
        if ( ! defined( $name ) ) {
            define( $name, $value );
        }
    }

    /**
     * Include required files.
     *
     * @return void
     */
    private function includes() {
        // Core includes.
        require_once PREFIX_INCLUDES_DIR . 'prefix-core-functions.php';
        require_once PREFIX_INCLUDES_DIR . 'class-prefix-post-types.php';
        require_once PREFIX_INCLUDES_DIR . 'class-prefix-taxonomies.php';
        require_once PREFIX_INCLUDES_DIR . 'class-prefix-shortcodes.php';
        require_once PREFIX_INCLUDES_DIR . 'class-prefix-ajax.php';
        
        // Admin includes.
        if ( is_admin() ) {
            require_once PREFIX_INCLUDES_DIR . 'admin/class-prefix-admin.php';
            require_once PREFIX_INCLUDES_DIR . 'admin/class-prefix-admin-settings.php';
            require_once PREFIX_INCLUDES_DIR . 'admin/class-prefix-admin-meta-boxes.php';
        }
        
        // Frontend includes.
        if ( ! is_admin() || wp_doing_ajax() ) {
            require_once PREFIX_INCLUDES_DIR . 'frontend/class-prefix-frontend.php';
        }
    }

    /**
     * Initialize hooks.
     *
     * @return void
     */
    private function init_hooks() {
        add_action( 'init', array( $this, 'init' ), 0 );
        add_action( 'init', array( 'Prefix_Post_Types', 'register' ) );
        add_action( 'init', array( 'Prefix_Taxonomies', 'register' ) );
        add_action( 'init', array( 'Prefix_Shortcodes', 'init' ) );
        add_action( 'widgets_init', array( $this, 'register_widgets' ) );
    }

    /**
     * Initialize plugin components.
     *
     * @return void
     */
    public function init() {
        /**
         * Fires before plugin initialization.
         *
         * @since 1.0.0
         */
        do_action( 'prefix_before_init' );
        
        // Initialize AJAX handler.
        $this->ajax = new Prefix_Ajax();
        
        // Initialize admin.
        if ( is_admin() ) {
            $this->admin = new Prefix_Admin();
        }
        
        // Initialize frontend.
        if ( ! is_admin() || wp_doing_ajax() ) {
            $this->frontend = new Prefix_Frontend();
        }
        
        /**
         * Fires after plugin initialization.
         *
         * @since 1.0.0
         */
        do_action( 'prefix_init' );
    }

    /**
     * Register widgets.
     *
     * @return void
     */
    public function register_widgets() {
        require_once PREFIX_INCLUDES_DIR . 'widgets/class-prefix-widget-example.php';
        register_widget( 'Prefix_Widget_Example' );
    }

    /**
     * Get plugin path.
     *
     * @return string
     */
    public function plugin_path() {
        return untrailingslashit( PREFIX_PLUGIN_DIR );
    }

    /**
     * Get plugin URL.
     *
     * @return string
     */
    public function plugin_url() {
        return untrailingslashit( PREFIX_PLUGIN_URL );
    }

    /**
     * Get template path.
     *
     * @return string
     */
    public function template_path() {
        /**
         * Filters the template path.
         *
         * @since 1.0.0
         * @param string $path Default template path.
         */
        return apply_filters( 'prefix_template_path', 'prefix-plugin-name/' );
    }

    /**
     * Get AJAX URL.
     *
     * @return string
     */
    public function ajax_url() {
        return admin_url( 'admin-ajax.php', 'relative' );
    }
}

/**
 * Main instance function.
 *
 * @return Prefix_Plugin_Name
 */
function PREFIX() {
    return Prefix_Plugin_Name::instance();
}
```

### Directory Structure

```
prefix-plugin-name/
├── assets/
│   ├── css/
│   │   ├── admin.css
│   │   ├── admin.min.css
│   │   ├── frontend.css
│   │   └── frontend.min.css
│   ├── js/
│   │   ├── admin.js
│   │   ├── admin.min.js
│   │   ├── frontend.js
│   │   └── frontend.min.js
│   ├── images/
│   └── fonts/
├── includes/
│   ├── admin/
│   │   ├── class-prefix-admin.php
│   │   ├── class-prefix-admin-settings.php
│   │   ├── class-prefix-admin-meta-boxes.php
│   │   └── views/
│   │       ├── html-admin-settings.php
│   │       └── html-admin-meta-box.php
│   ├── frontend/
│   │   ├── class-prefix-frontend.php
│   │   └── class-prefix-frontend-scripts.php
│   ├── widgets/
│   │   └── class-prefix-widget-example.php
│   ├── abstracts/
│   │   └── abstract-prefix-widget.php
│   ├── interfaces/
│   │   └── interface-prefix-data.php
│   ├── class-prefix-autoloader.php
│   ├── class-prefix-install.php
│   ├── class-prefix-post-types.php
│   ├── class-prefix-taxonomies.php
│   ├── class-prefix-shortcodes.php
│   ├── class-prefix-ajax.php
│   └── prefix-core-functions.php
├── languages/
│   └── prefix-plugin-name.pot
├── templates/
│   ├── single-prefix-post.php
│   ├── archive-prefix-post.php
│   └── shortcodes/
│       └── shortcode-example.php
├── vendor/
├── .editorconfig
├── .gitignore
├── composer.json
├── package.json
├── phpcs.xml.dist
├── README.txt
├── readme.md
├── CHANGELOG.md
├── LICENSE.txt
├── uninstall.php
└── prefix-plugin-name.php
```

---

## WooCommerce Development Standards

> **Reference**: https://developer.woocommerce.com/docs/

### WooCommerce Plugin Header

```php
<?php
/**
 * Plugin Name:       Prefix WooCommerce Extension
 * Plugin URI:        https://example.com/prefix-woocommerce-extension
 * Description:       Extends WooCommerce with additional functionality.
 * Version:           1.0.0
 * Requires at least: 5.8
 * Requires PHP:      7.4
 * Author:            Your Name
 * Author URI:        https://example.com
 * License:           GPL v2 or later
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain:       prefix-wc-extension
 * Domain Path:       /languages
 *
 * WC requires at least: 7.0
 * WC tested up to:      8.5
 *
 * Woo: 12345:abcdef1234567890abcdef1234567890
 *
 * @package Prefix_WC_Extension
 */

// Exit if accessed directly.
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Check if WooCommerce is active.
 *
 * @return bool
 */
function prefix_wc_is_woocommerce_active() {
    return class_exists( 'WooCommerce' );
}

/**
 * WooCommerce not active notice.
 *
 * @return void
 */
function prefix_wc_woocommerce_missing_notice() {
    ?>
    <div class="notice notice-error">
        <p>
            <?php
            printf(
                /* translators: %s: WooCommerce plugin URL */
                wp_kses(
                    __( 'Prefix WooCommerce Extension requires WooCommerce to be installed and active. You can download <a href="%s" target="_blank">WooCommerce</a> here.', 'prefix-wc-extension' ),
                    array( 'a' => array( 'href' => array(), 'target' => array() ) )
                ),
                'https://woocommerce.com/'
            );
            ?>
        </p>
    </div>
    <?php
}

/**
 * Initialize plugin.
 *
 * @return void
 */
function prefix_wc_init() {
    if ( ! prefix_wc_is_woocommerce_active() ) {
        add_action( 'admin_notices', 'prefix_wc_woocommerce_missing_notice' );
        return;
    }
    
    // Declare HPOS compatibility.
    add_action( 'before_woocommerce_init', function() {
        if ( class_exists( \Automattic\WooCommerce\Utilities\FeaturesUtil::class ) ) {
            \Automattic\WooCommerce\Utilities\FeaturesUtil::declare_compatibility(
                'custom_order_tables',
                __FILE__,
                true
            );
        }
    } );
    
    // Declare Cart/Checkout Blocks compatibility.
    add_action( 'before_woocommerce_init', function() {
        if ( class_exists( '\Automattic\WooCommerce\Utilities\FeaturesUtil' ) ) {
            \Automattic\WooCommerce\Utilities\FeaturesUtil::declare_compatibility(
                'cart_checkout_blocks',
                __FILE__,
                true
            );
        }
    } );
    
    // Load main class.
    require_once plugin_dir_path( __FILE__ ) . 'includes/class-prefix-wc-extension.php';
    Prefix_WC_Extension::instance();
}
add_action( 'plugins_loaded', 'prefix_wc_init' );
```

### WooCommerce Hooks Best Practices

```php
<?php
/**
 * WooCommerce hooks implementation examples.
 *
 * @package Prefix_WC_Extension
 */

// Exit if accessed directly.
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Class Prefix_WC_Hooks
 *
 * Demonstrates proper WooCommerce hook usage.
 */
class Prefix_WC_Hooks {

    /**
     * Constructor.
     */
    public function __construct() {
        $this->init_hooks();
    }

    /**
     * Initialize hooks.
     *
     * @return void
     */
    private function init_hooks() {
        // Product hooks.
        add_action( 'woocommerce_before_single_product', array( $this, 'before_single_product' ) );
        add_action( 'woocommerce_after_single_product', array( $this, 'after_single_product' ) );
        add_action( 'woocommerce_single_product_summary', array( $this, 'custom_product_content' ), 25 );
        
        // Cart hooks.
        add_action( 'woocommerce_before_cart', array( $this, 'before_cart' ) );
        add_action( 'woocommerce_cart_calculate_fees', array( $this, 'add_custom_fee' ) );
        add_filter( 'woocommerce_cart_item_price', array( $this, 'modify_cart_item_price' ), 10, 3 );
        
        // Checkout hooks.
        add_action( 'woocommerce_before_checkout_form', array( $this, 'before_checkout_form' ), 10 );
        add_action( 'woocommerce_checkout_fields', array( $this, 'customize_checkout_fields' ) );
        add_action( 'woocommerce_checkout_process', array( $this, 'validate_checkout_fields' ) );
        add_action( 'woocommerce_checkout_update_order_meta', array( $this, 'save_custom_checkout_fields' ) );
        
        // Order hooks.
        add_action( 'woocommerce_order_status_changed', array( $this, 'order_status_changed' ), 10, 4 );
        add_action( 'woocommerce_thankyou', array( $this, 'custom_thankyou_content' ), 10, 1 );
        
        // Product filters.
        add_filter( 'woocommerce_product_get_price', array( $this, 'modify_product_price' ), 10, 2 );
        add_filter( 'woocommerce_product_get_sale_price', array( $this, 'modify_sale_price' ), 10, 2 );
        add_filter( 'woocommerce_is_purchasable', array( $this, 'check_is_purchasable' ), 10, 2 );
        
        // Admin hooks.
        add_action( 'woocommerce_product_options_general_product_data', array( $this, 'add_custom_product_fields' ) );
        add_action( 'woocommerce_process_product_meta', array( $this, 'save_custom_product_fields' ) );
        add_action( 'woocommerce_admin_order_data_after_billing_address', array( $this, 'display_custom_order_data' ) );
    }

    /**
     * Add custom content before single product.
     *
     * @return void
     */
    public function before_single_product() {
        global $product;
        
        if ( ! $product instanceof WC_Product ) {
            return;
        }
        
        /**
         * Filters whether to show custom content before product.
         *
         * @since 1.0.0
         * @param bool       $show    Whether to show content.
         * @param WC_Product $product Product object.
         */
        if ( ! apply_filters( 'prefix_wc_show_before_product_content', true, $product ) ) {
            return;
        }
        
        wc_get_template(
            'single-product/before-product.php',
            array( 'product' => $product ),
            '',
            PREFIX_WC_EXTENSION_TEMPLATE_PATH
        );
    }

    /**
     * Add custom fee to cart.
     *
     * @param WC_Cart $cart Cart object.
     * @return void
     */
    public function add_custom_fee( $cart ) {
        if ( is_admin() && ! defined( 'DOING_AJAX' ) ) {
            return;
        }
        
        $custom_fee = $this->calculate_custom_fee( $cart );
        
        if ( $custom_fee > 0 ) {
            $cart->add_fee(
                __( 'Custom Fee', 'prefix-wc-extension' ),
                $custom_fee,
                true, // Taxable.
                '' // Tax class (empty for standard).
            );
        }
    }

    /**
     * Calculate custom fee based on cart contents.
     *
     * @param WC_Cart $cart Cart object.
     * @return float Fee amount.
     */
    private function calculate_custom_fee( $cart ) {
        $fee = 0;
        
        foreach ( $cart->get_cart() as $cart_item_key => $cart_item ) {
            $product = $cart_item['data'];
            
            if ( 'yes' === $product->get_meta( '_prefix_apply_custom_fee' ) ) {
                $fee += 5.00 * $cart_item['quantity'];
            }
        }
        
        /**
         * Filters the custom fee amount.
         *
         * @since 1.0.0
         * @param float   $fee  Fee amount.
         * @param WC_Cart $cart Cart object.
         */
        return apply_filters( 'prefix_wc_custom_fee_amount', $fee, $cart );
    }

    /**
     * Customize checkout fields.
     *
     * @param array $fields Checkout fields.
     * @return array Modified fields.
     */
    public function customize_checkout_fields( $fields ) {
        // Add custom field.
        $fields['billing']['prefix_custom_field'] = array(
            'type'        => 'text',
            'label'       => __( 'Custom Field', 'prefix-wc-extension' ),
            'placeholder' => __( 'Enter value', 'prefix-wc-extension' ),
            'required'    => false,
            'class'       => array( 'form-row-wide' ),
            'priority'    => 120,
        );
        
        // Modify existing field.
        if ( isset( $fields['billing']['billing_phone'] ) ) {
            $fields['billing']['billing_phone']['required'] = true;
        }
        
        return $fields;
    }

    /**
     * Validate custom checkout fields.
     *
     * @return void
     */
    public function validate_checkout_fields() {
        $custom_field = isset( $_POST['prefix_custom_field'] ) 
            ? sanitize_text_field( wp_unslash( $_POST['prefix_custom_field'] ) ) 
            : '';
        
        // Validate nonce is handled by WooCommerce checkout.
        
        if ( ! empty( $custom_field ) && strlen( $custom_field ) < 3 ) {
            wc_add_notice(
                __( 'Custom field must be at least 3 characters.', 'prefix-wc-extension' ),
                'error'
            );
        }
    }

    /**
     * Save custom checkout fields to order.
     *
     * @param int $order_id Order ID.
     * @return void
     */
    public function save_custom_checkout_fields( $order_id ) {
        if ( isset( $_POST['prefix_custom_field'] ) ) {
            $order = wc_get_order( $order_id );
            
            if ( $order ) {
                $order->update_meta_data(
                    '_prefix_custom_field',
                    sanitize_text_field( wp_unslash( $_POST['prefix_custom_field'] ) )
                );
                $order->save();
            }
        }
    }

    /**
     * Handle order status change.
     *
     * @param int      $order_id   Order ID.
     * @param string   $old_status Old status.
     * @param string   $new_status New status.
     * @param WC_Order $order      Order object.
     * @return void
     */
    public function order_status_changed( $order_id, $old_status, $new_status, $order ) {
        // Process specific status transitions.
        if ( 'completed' === $new_status && 'processing' === $old_status ) {
            /**
             * Fires when order transitions from processing to completed.
             *
             * @since 1.0.0
             * @param int      $order_id Order ID.
             * @param WC_Order $order    Order object.
             */
            do_action( 'prefix_wc_order_completed_from_processing', $order_id, $order );
            
            // Custom logic here.
            $this->send_custom_notification( $order );
        }
    }

    /**
     * Add custom product fields in admin.
     *
     * @return void
     */
    public function add_custom_product_fields() {
        global $post;
        
        echo '<div class="options_group">';
        
        woocommerce_wp_text_input(
            array(
                'id'          => '_prefix_custom_text',
                'label'       => __( 'Custom Text', 'prefix-wc-extension' ),
                'placeholder' => __( 'Enter custom text', 'prefix-wc-extension' ),
                'description' => __( 'This is a custom text field.', 'prefix-wc-extension' ),
                'desc_tip'    => true,
            )
        );
        
        woocommerce_wp_checkbox(
            array(
                'id'          => '_prefix_apply_custom_fee',
                'label'       => __( 'Apply Custom Fee', 'prefix-wc-extension' ),
                'description' => __( 'Check to apply custom fee to this product.', 'prefix-wc-extension' ),
            )
        );
        
        woocommerce_wp_select(
            array(
                'id'          => '_prefix_custom_select',
                'label'       => __( 'Custom Option', 'prefix-wc-extension' ),
                'options'     => array(
                    ''       => __( 'Select option', 'prefix-wc-extension' ),
                    'option1' => __( 'Option 1', 'prefix-wc-extension' ),
                    'option2' => __( 'Option 2', 'prefix-wc-extension' ),
                    'option3' => __( 'Option 3', 'prefix-wc-extension' ),
                ),
            )
        );
        
        echo '</div>';
    }

    /**
     * Save custom product fields.
     *
     * @param int $post_id Post ID.
     * @return void
     */
    public function save_custom_product_fields( $post_id ) {
        // Verify nonce.
        if ( ! isset( $_POST['woocommerce_meta_nonce'] ) || 
             ! wp_verify_nonce( sanitize_text_field( wp_unslash( $_POST['woocommerce_meta_nonce'] ) ), 'woocommerce_save_data' ) ) {
            return;
        }
        
        $product = wc_get_product( $post_id );
        
        if ( ! $product ) {
            return;
        }
        
        // Save text field.
        if ( isset( $_POST['_prefix_custom_text'] ) ) {
            $product->update_meta_data(
                '_prefix_custom_text',
                sanitize_text_field( wp_unslash( $_POST['_prefix_custom_text'] ) )
            );
        }
        
        // Save checkbox.
        $product->update_meta_data(
            '_prefix_apply_custom_fee',
            isset( $_POST['_prefix_apply_custom_fee'] ) ? 'yes' : 'no'
        );
        
        // Save select.
        if ( isset( $_POST['_prefix_custom_select'] ) ) {
            $product->update_meta_data(
                '_prefix_custom_select',
                sanitize_text_field( wp_unslash( $_POST['_prefix_custom_select'] ) )
            );
        }
        
        $product->save();
    }

    /**
     * Send custom notification.
     *
     * @param WC_Order $order Order object.
     * @return void
     */
    private function send_custom_notification( $order ) {
        // Implementation.
    }
}
```

### WooCommerce Template Overrides

```php
<?php
/**
 * Custom product template.
 *
 * This template can be overridden by copying it to yourtheme/prefix-wc-extension/single-product/custom-content.php.
 *
 * HOWEVER, on occasion we will need to update template files and you
 * (the theme developer) will need to copy the new files to your theme to
 * maintain compatibility.
 *
 * @see     https://example.com/document/template-structure/
 * @package Prefix_WC_Extension/Templates
 * @version 1.0.0
 */

// Exit if accessed directly.
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Before custom content hook.
 *
 * @hooked prefix_wc_before_custom_content - 10
 */
do_action( 'prefix_wc_before_custom_content', $product );

?>
<div class="prefix-wc-custom-content">
    <h3><?php esc_html_e( 'Custom Content', 'prefix-wc-extension' ); ?></h3>
    
    <?php if ( $custom_data ) : ?>
        <div class="prefix-wc-custom-data">
            <?php echo wp_kses_post( $custom_data ); ?>
        </div>
    <?php endif; ?>
    
    <?php
    /**
     * Custom content hook.
     *
     * @hooked prefix_wc_custom_content_items - 10
     */
    do_action( 'prefix_wc_custom_content', $product, $args );
    ?>
</div>
<?php

/**
 * After custom content hook.
 *
 * @hooked prefix_wc_after_custom_content - 10
 */
do_action( 'prefix_wc_after_custom_content', $product );
```

---

## Block Editor (Gutenberg) Development

> **Reference**: https://developer.wordpress.org/block-editor/

### Block Registration (PHP)

```php
<?php
/**
 * Block registration and server-side functionality.
 *
 * @package Prefix_Blocks
 */

// Exit if accessed directly.
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Register blocks.
 *
 * @return void
 */
function prefix_register_blocks() {
    // Register block with block.json.
    register_block_type( PREFIX_PLUGIN_DIR . 'blocks/custom-block' );
    
    // Register dynamic block.
    register_block_type(
        'prefix/dynamic-block',
        array(
            'api_version'     => 3,
            'title'           => __( 'Dynamic Block', 'textdomain' ),
            'description'     => __( 'A dynamic block with server-side rendering.', 'textdomain' ),
            'category'        => 'widgets',
            'icon'            => 'admin-generic',
            'supports'        => array(
                'html'         => false,
                'align'        => array( 'wide', 'full' ),
                'anchor'       => true,
                'customClassName' => true,
                'color'        => array(
                    'background' => true,
                    'text'       => true,
                    'link'       => true,
                ),
                'spacing'      => array(
                    'margin'  => true,
                    'padding' => true,
                ),
                'typography'   => array(
                    'fontSize'   => true,
                    'lineHeight' => true,
                ),
            ),
            'attributes'      => array(
                'title' => array(
                    'type'    => 'string',
                    'default' => '',
                ),
                'count' => array(
                    'type'    => 'number',
                    'default' => 5,
                ),
                'showImages' => array(
                    'type'    => 'boolean',
                    'default' => true,
                ),
                'categories' => array(
                    'type'    => 'array',
                    'default' => array(),
                    'items'   => array(
                        'type' => 'number',
                    ),
                ),
            ),
            'editor_script'   => 'prefix-dynamic-block-editor',
            'editor_style'    => 'prefix-dynamic-block-editor-style',
            'style'           => 'prefix-dynamic-block-style',
            'render_callback' => 'prefix_render_dynamic_block',
        )
    );
}
add_action( 'init', 'prefix_register_blocks' );

/**
 * Render dynamic block.
 *
 * @param array    $attributes Block attributes.
 * @param string   $content    Block content.
 * @param WP_Block $block      Block instance.
 * @return string Rendered block HTML.
 */
function prefix_render_dynamic_block( $attributes, $content, $block ) {
    $attributes = wp_parse_args(
        $attributes,
        array(
            'title'      => '',
            'count'      => 5,
            'showImages' => true,
            'categories' => array(),
        )
    );
    
    // Build query args.
    $query_args = array(
        'post_type'      => 'post',
        'posts_per_page' => absint( $attributes['count'] ),
        'post_status'    => 'publish',
    );
    
    if ( ! empty( $attributes['categories'] ) ) {
        $query_args['category__in'] = array_map( 'absint', $attributes['categories'] );
    }
    
    /**
     * Filters query args for dynamic block.
     *
     * @since 1.0.0
     * @param array $query_args Query arguments.
     * @param array $attributes Block attributes.
     */
    $query_args = apply_filters( 'prefix_dynamic_block_query_args', $query_args, $attributes );
    
    $query = new WP_Query( $query_args );
    
    // Get wrapper attributes.
    $wrapper_attributes = get_block_wrapper_attributes(
        array(
            'class' => 'prefix-dynamic-block',
        )
    );
    
    ob_start();
    ?>
    <div <?php echo $wrapper_attributes; // phpcs:ignore WordPress.Security.EscapeOutput.OutputNotEscaped ?>>
        <?php if ( ! empty( $attributes['title'] ) ) : ?>
            <h2 class="prefix-dynamic-block__title">
                <?php echo esc_html( $attributes['title'] ); ?>
            </h2>
        <?php endif; ?>
        
        <?php if ( $query->have_posts() ) : ?>
            <div class="prefix-dynamic-block__items">
                <?php
                while ( $query->have_posts() ) :
                    $query->the_post();
                    ?>
                    <article class="prefix-dynamic-block__item">
                        <?php if ( $attributes['showImages'] && has_post_thumbnail() ) : ?>
                            <div class="prefix-dynamic-block__image">
                                <?php the_post_thumbnail( 'medium' ); ?>
                            </div>
                        <?php endif; ?>
                        
                        <h3 class="prefix-dynamic-block__item-title">
                            <a href="<?php the_permalink(); ?>">
                                <?php the_title(); ?>
                            </a>
                        </h3>
                        
                        <div class="prefix-dynamic-block__excerpt">
                            <?php the_excerpt(); ?>
                        </div>
                    </article>
                    <?php
                endwhile;
                wp_reset_postdata();
                ?>
            </div>
        <?php else : ?>
            <p class="prefix-dynamic-block__no-results">
                <?php esc_html_e( 'No posts found.', 'textdomain' ); ?>
            </p>
        <?php endif; ?>
    </div>
    <?php
    return ob_get_clean();
}

/**
 * Register block scripts and styles.
 *
 * @return void
 */
function prefix_register_block_assets() {
    $asset_file = include PREFIX_PLUGIN_DIR . 'build/dynamic-block/index.asset.php';
    
    // Editor script.
    wp_register_script(
        'prefix-dynamic-block-editor',
        PREFIX_PLUGIN_URL . 'build/dynamic-block/index.js',
        $asset_file['dependencies'],
        $asset_file['version'],
        true
    );
    
    // Localize script.
    wp_localize_script(
        'prefix-dynamic-block-editor',
        'prefixBlockData',
        array(
            'restUrl'  => rest_url( 'prefix/v1/' ),
            'nonce'    => wp_create_nonce( 'wp_rest' ),
            'homeUrl'  => home_url(),
        )
    );
    
    // Editor styles.
    wp_register_style(
        'prefix-dynamic-block-editor-style',
        PREFIX_PLUGIN_URL . 'build/dynamic-block/editor.css',
        array( 'wp-edit-blocks' ),
        $asset_file['version']
    );
    
    // Frontend styles.
    wp_register_style(
        'prefix-dynamic-block-style',
        PREFIX_PLUGIN_URL . 'build/dynamic-block/style.css',
        array(),
        $asset_file['version']
    );
}
add_action( 'init', 'prefix_register_block_assets' );
```

### block.json (Modern Approach)

```json
{
    "$schema": "https://schemas.wp.org/trunk/block.json",
    "apiVersion": 3,
    "name": "prefix/custom-block",
    "version": "1.0.0",
    "title": "Custom Block",
    "category": "widgets",
    "description": "A custom block with full feature support.",
    "keywords": ["custom", "block", "example"],
    "textdomain": "textdomain",
    "attributes": {
        "title": {
            "type": "string",
            "default": ""
        },
        "content": {
            "type": "string",
            "default": ""
        },
        "alignment": {
            "type": "string",
            "default": "left"
        },
        "backgroundColor": {
            "type": "string"
        },
        "textColor": {
            "type": "string"
        }
    },
    "supports": {
        "html": false,
        "align": ["wide", "full"],
        "anchor": true,
        "customClassName": true,
        "color": {
            "background": true,
            "text": true,
            "link": true,
            "gradients": true
        },
        "spacing": {
            "margin": true,
            "padding": true,
            "blockGap": true
        },
        "typography": {
            "fontSize": true,
            "lineHeight": true,
            "textDecoration": true,
            "fontStyle": true,
            "fontWeight": true,
            "letterSpacing": true
        },
        "__experimentalBorder": {
            "color": true,
            "radius": true,
            "style": true,
            "width": true
        }
    },
    "editorScript": "file:./index.js",
    "editorStyle": "file:./editor.css",
    "style": "file:./style.css",
    "render": "file:./render.php",
    "viewScript": "file:./view.js"
}
```

---

## Security Best Practices

> **Reference**: https://developer.wordpress.org/plugins/security/

### Data Validation, Sanitization, and Escaping

```php
<?php
/**
 * Security best practices demonstration.
 *
 * @package Prefix_Security
 */

// Exit if accessed directly.
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Class Prefix_Security_Handler
 *
 * Demonstrates proper security practices.
 */
class Prefix_Security_Handler {

    /**
     * Process form submission with proper security.
     *
     * @return void
     */
    public function process_form_submission() {
        // 1. Verify nonce.
        if ( ! isset( $_POST['prefix_nonce'] ) || 
             ! wp_verify_nonce( sanitize_text_field( wp_unslash( $_POST['prefix_nonce'] ) ), 'prefix_form_action' ) ) {
            wp_die(
                esc_html__( 'Security check failed.', 'textdomain' ),
                esc_html__( 'Error', 'textdomain' ),
                array( 'response' => 403 )
            );
        }
        
        // 2. Check user capabilities.
        if ( ! current_user_can( 'edit_posts' ) ) {
            wp_die(
                esc_html__( 'You do not have permission to perform this action.', 'textdomain' ),
                esc_html__( 'Error', 'textdomain' ),
                array( 'response' => 403 )
            );
        }
        
        // 3. Sanitize all input data.
        $sanitized_data = array(
            'title'       => isset( $_POST['title'] ) 
                ? sanitize_text_field( wp_unslash( $_POST['title'] ) ) 
                : '',
            'content'     => isset( $_POST['content'] ) 
                ? wp_kses_post( wp_unslash( $_POST['content'] ) ) 
                : '',
            'email'       => isset( $_POST['email'] ) 
                ? sanitize_email( wp_unslash( $_POST['email'] ) ) 
                : '',
            'url'         => isset( $_POST['url'] ) 
                ? esc_url_raw( wp_unslash( $_POST['url'] ) ) 
                : '',
            'number'      => isset( $_POST['number'] ) 
                ? absint( $_POST['number'] ) 
                : 0,
            'float'       => isset( $_POST['float'] ) 
                ? (float) $_POST['float'] 
                : 0.0,
            'textarea'    => isset( $_POST['textarea'] ) 
                ? sanitize_textarea_field( wp_unslash( $_POST['textarea'] ) ) 
                : '',
            'filename'    => isset( $_POST['filename'] ) 
                ? sanitize_file_name( wp_unslash( $_POST['filename'] ) ) 
                : '',
            'key'         => isset( $_POST['key'] ) 
                ? sanitize_key( wp_unslash( $_POST['key'] ) ) 
                : '',
            'html_class'  => isset( $_POST['html_class'] ) 
                ? sanitize_html_class( wp_unslash( $_POST['html_class'] ) ) 
                : '',
            'options'     => isset( $_POST['options'] ) && is_array( $_POST['options'] )
                ? array_map( 'sanitize_text_field', wp_unslash( $_POST['options'] ) )
                : array(),
        );
        
        // 4. Validate data.
        $errors = array();
        
        if ( empty( $sanitized_data['title'] ) ) {
            $errors[] = __( 'Title is required.', 'textdomain' );
        }
        
        if ( ! is_email( $sanitized_data['email'] ) ) {
            $errors[] = __( 'Please enter a valid email address.', 'textdomain' );
        }
        
        if ( $sanitized_data['number'] < 1 || $sanitized_data['number'] > 100 ) {
            $errors[] = __( 'Number must be between 1 and 100.', 'textdomain' );
        }
        
        if ( ! empty( $errors ) ) {
            // Handle errors.
            return $errors;
        }
        
        // 5. Process validated data.
        $this->save_data( $sanitized_data );
    }

    /**
     * Display data with proper escaping.
     *
     * @param array $data Data to display.
     * @return void
     */
    public function display_data( $data ) {
        ?>
        <div class="prefix-data-display">
            <!-- Escape text output -->
            <h2><?php echo esc_html( $data['title'] ); ?></h2>
            
            <!-- Allow specific HTML -->
            <div class="content">
                <?php echo wp_kses_post( $data['content'] ); ?>
            </div>
            
            <!-- Escape attributes -->
            <a href="<?php echo esc_url( $data['url'] ); ?>" 
               title="<?php echo esc_attr( $data['title'] ); ?>"
               class="<?php echo esc_attr( $data['html_class'] ); ?>">
                <?php echo esc_html( $data['link_text'] ); ?>
            </a>
            
            <!-- Escape JavaScript values -->
            <script>
                var prefixData = <?php echo wp_json_encode( array(
                    'title'   => $data['title'],
                    'ajaxUrl' => admin_url( 'admin-ajax.php' ),
                    'nonce'   => wp_create_nonce( 'prefix_ajax_nonce' ),
                ) ); ?>;
            </script>
            
            <!-- Escape for inline JavaScript -->
            <button onclick="handleClick('<?php echo esc_js( $data['id'] ); ?>')">
                <?php esc_html_e( 'Click Me', 'textdomain' ); ?>
            </button>
            
            <!-- Escape translation with placeholders -->
            <p>
                <?php
                printf(
                    /* translators: 1: User name, 2: Date */
                    esc_html__( 'Created by %1$s on %2$s.', 'textdomain' ),
                    esc_html( $data['author'] ),
                    esc_html( $data['date'] )
                );
                ?>
            </p>
            
            <!-- wp_kses with custom allowed HTML -->
            <?php
            $allowed_html = array(
                'a'      => array(
                    'href'   => array(),
                    'title'  => array(),
                    'target' => array(),
                    'rel'    => array(),
                ),
                'strong' => array(),
                'em'     => array(),
                'br'     => array(),
            );
            echo wp_kses( $data['rich_content'], $allowed_html );
            ?>
        </div>
        <?php
    }

    /**
     * Create nonce field for form.
     *
     * @return void
     */
    public function render_form() {
        ?>
        <form method="post" action="">
            <?php wp_nonce_field( 'prefix_form_action', 'prefix_nonce' ); ?>
            
            <input type="text" name="title" value="">
            <textarea name="content"></textarea>
            
            <?php submit_button( __( 'Submit', 'textdomain' ) ); ?>
        </form>
        <?php
    }

    /**
     * Secure AJAX handler.
     *
     * @return void
     */
    public function ajax_handler() {
        // Check nonce.
        check_ajax_referer( 'prefix_ajax_nonce', 'nonce' );
        
        // Check capabilities.
        if ( ! current_user_can( 'edit_posts' ) ) {
            wp_send_json_error(
                array( 'message' => __( 'Permission denied.', 'textdomain' ) ),
                403
            );
        }
        
        // Get and sanitize data.
        $item_id = isset( $_POST['item_id'] ) ? absint( $_POST['item_id'] ) : 0;
        
        if ( ! $item_id ) {
            wp_send_json_error(
                array( 'message' => __( 'Invalid item ID.', 'textdomain' ) ),
                400
            );
        }
        
        // Process request.
        $result = $this->process_item( $item_id );
        
        if ( is_wp_error( $result ) ) {
            wp_send_json_error(
                array( 'message' => $result->get_error_message() ),
                400
            );
        }
        
        wp_send_json_success( array(
            'message' => __( 'Item processed successfully.', 'textdomain' ),
            'data'    => $result,
        ) );
    }

    /**
     * Safe database query with prepared statements.
     *
     * @param int    $user_id   User ID.
     * @param string $meta_key  Meta key.
     * @param mixed  $meta_value Meta value.
     * @return bool|int
     */
    public function safe_database_query( $user_id, $meta_key, $meta_value ) {
        global $wpdb;
        
        // Always use prepared statements.
        $result = $wpdb->query(
            $wpdb->prepare(
                "UPDATE {$wpdb->usermeta} SET meta_value = %s WHERE user_id = %d AND meta_key = %s",
                $meta_value,
                $user_id,
                $meta_key
            )
        );
        
        return $result;
    }

    /**
     * Safe file upload handling.
     *
     * @param array $file Uploaded file data.
     * @return int|WP_Error Attachment ID or error.
     */
    public function handle_file_upload( $file ) {
        // Check nonce and capability first.
        if ( ! current_user_can( 'upload_files' ) ) {
            return new WP_Error( 'permission_denied', __( 'You cannot upload files.', 'textdomain' ) );
        }
        
        // Verify file type.
        $allowed_types = array( 'image/jpeg', 'image/png', 'image/gif', 'application/pdf' );
        
        $file_type = wp_check_filetype( $file['name'] );
        
        if ( ! in_array( $file_type['type'], $allowed_types, true ) ) {
            return new WP_Error( 'invalid_type', __( 'File type not allowed.', 'textdomain' ) );
        }
        
        // Check file size (5MB max).
        $max_size = 5 * 1024 * 1024;
        
        if ( $file['size'] > $max_size ) {
            return new WP_Error( 'file_too_large', __( 'File size exceeds limit.', 'textdomain' ) );
        }
        
        // Use WordPress media handling.
        require_once ABSPATH . 'wp-admin/includes/image.php';
        require_once ABSPATH . 'wp-admin/includes/file.php';
        require_once ABSPATH . 'wp-admin/includes/media.php';
        
        $attachment_id = media_handle_upload( 'prefix_file', 0 );
        
        return $attachment_id;
    }
}
```

---

## Internationalization & Localization

> **Reference**: https://developer.wordpress.org/plugins/internationalization/

### Translation Functions

```php
<?php
/**
 * Internationalization examples.
 *
 * @package Prefix_i18n
 */

// Exit if accessed directly.
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Load textdomain.
 *
 * @return void
 */
function prefix_load_textdomain() {
    load_plugin_textdomain(
        'prefix-plugin',
        false,
        dirname( plugin_basename( __FILE__ ) ) . '/languages/'
    );
}
add_action( 'init', 'prefix_load_textdomain' );

/**
 * Demonstration of translation functions.
 *
 * @return void
 */
function prefix_i18n_examples() {
    // Basic string translation.
    $text = __( 'This is translatable text.', 'prefix-plugin' );
    
    // Echo translated string.
    _e( 'This text is echoed.', 'prefix-plugin' );
    
    // Escaped translation for HTML context.
    echo esc_html__( 'This is escaped.', 'prefix-plugin' );
    esc_html_e( 'This is escaped and echoed.', 'prefix-plugin' );
    
    // Escaped for attribute context.
    $attr = esc_attr__( 'Attribute text', 'prefix-plugin' );
    esc_attr_e( 'Echoed attribute', 'prefix-plugin' );
    
    // Pluralization.
    $count = 5;
    $message = sprintf(
        /* translators: %d: Number of items */
        _n(
            '%d item found.',
            '%d items found.',
            $count,
            'prefix-plugin'
        ),
        $count
    );
    
    // Context-specific translations (for disambiguation).
    $post_noun = _x( 'Post', 'noun (blog post)', 'prefix-plugin' );
    $post_verb = _x( 'Post', 'verb (to post)', 'prefix-plugin' );
    
    // Context with escaping.
    $title = esc_html_x( 'Title', 'column name', 'prefix-plugin' );
    
    // Pluralization with context.
    $comment_count = 3;
    $comments_text = _nx(
        '%d Comment',
        '%d Comments',
        $comment_count,
        'number of comments',
        'prefix-plugin'
    );
    
    // Number formatting.
    $number = number_format_i18n( 1234567.89, 2 );
    
    // Date formatting.
    $date = date_i18n( get_option( 'date_format' ), strtotime( '2024-01-15' ) );
    
    // Translators comments for complex strings.
    printf(
        /* translators: 1: User name, 2: Post title, 3: Date */
        esc_html__( '%1$s published "%2$s" on %3$s.', 'prefix-plugin' ),
        esc_html( $user_name ),
        esc_html( $post_title ),
        esc_html( $formatted_date )
    );
    
    // HTML in translations (use with caution).
    printf(
        wp_kses(
            /* translators: %s: Link URL */
            __( 'Please visit our <a href="%s">documentation</a> for more information.', 'prefix-plugin' ),
            array( 'a' => array( 'href' => array() ) )
        ),
        esc_url( $doc_url )
    );
    
    // JavaScript translations (registered separately).
    wp_set_script_translations(
        'prefix-editor-script',
        'prefix-plugin',
        PREFIX_PLUGIN_DIR . 'languages'
    );
}
```

### JavaScript Translations

```javascript
/**
 * JavaScript internationalization.
 */
import { __ } from '@wordpress/i18n';
import { _n, _x, sprintf } from '@wordpress/i18n';

// Basic translation.
const title = __( 'Block Title', 'prefix-plugin' );

// With placeholder.
const message = sprintf(
    /* translators: %s: User name */
    __( 'Hello, %s!', 'prefix-plugin' ),
    userName
);

// Pluralization.
const itemsLabel = sprintf(
    /* translators: %d: Number of items */
    _n(
        '%d item',
        '%d items',
        itemCount,
        'prefix-plugin'
    ),
    itemCount
);

// Context-specific.
const orderNoun = _x( 'Order', 'noun (purchase order)', 'prefix-plugin' );
const orderVerb = _x( 'Order', 'verb (to order)', 'prefix-plugin' );
```

---

## REST API Development

> **Reference**: https://developer.wordpress.org/rest-api/

### Custom REST API Endpoints

```php
<?php
/**
 * REST API controller.
 *
 * @package Prefix_REST
 */

// Exit if accessed directly.
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Class Prefix_REST_Controller
 *
 * Handles custom REST API endpoints.
 */
class Prefix_REST_Controller extends WP_REST_Controller {

    /**
     * Namespace.
     *
     * @var string
     */
    protected $namespace = 'prefix/v1';

    /**
     * Resource name.
     *
     * @var string
     */
    protected $rest_base = 'items';

    /**
     * Register routes.
     *
     * @return void
     */
    public function register_routes() {
        // Collection routes.
        register_rest_route(
            $this->namespace,
            '/' . $this->rest_base,
            array(
                array(
                    'methods'             => WP_REST_Server::READABLE,
                    'callback'            => array( $this, 'get_items' ),
                    'permission_callback' => array( $this, 'get_items_permissions_check' ),
                    'args'                => $this->get_collection_params(),
                ),
                array(
                    'methods'             => WP_REST_Server::CREATABLE,
                    'callback'            => array( $this, 'create_item' ),
                    'permission_callback' => array( $this, 'create_item_permissions_check' ),
                    'args'                => $this->get_endpoint_args_for_item_schema( WP_REST_Server::CREATABLE ),
                ),
                'schema' => array( $this, 'get_public_item_schema' ),
            )
        );
        
        // Single item routes.
        register_rest_route(
            $this->namespace,
            '/' . $this->rest_base . '/(?P<id>[\d]+)',
            array(
                array(
                    'methods'             => WP_REST_Server::READABLE,
                    'callback'            => array( $this, 'get_item' ),
                    'permission_callback' => array( $this, 'get_item_permissions_check' ),
                    'args'                => array(
                        'context' => $this->get_context_param( array( 'default' => 'view' ) ),
                    ),
                ),
                array(
                    'methods'             => WP_REST_Server::EDITABLE,
                    'callback'            => array( $this, 'update_item' ),
                    'permission_callback' => array( $this, 'update_item_permissions_check' ),
                    'args'                => $this->get_endpoint_args_for_item_schema( WP_REST_Server::EDITABLE ),
                ),
                array(
                    'methods'             => WP_REST_Server::DELETABLE,
                    'callback'            => array( $this, 'delete_item' ),
                    'permission_callback' => array( $this, 'delete_item_permissions_check' ),
                    'args'                => array(
                        'force' => array(
                            'default'     => false,
                            'description' => __( 'Whether to bypass trash and force deletion.', 'prefix-plugin' ),
                            'type'        => 'boolean',
                        ),
                    ),
                ),
                'schema' => array( $this, 'get_public_item_schema' ),
            )
        );
    }

    /**
     * Get collection of items.
     *
     * @param WP_REST_Request $request Full details about the request.
     * @return WP_REST_Response|WP_Error Response object or error.
     */
    public function get_items( $request ) {
        $params = $request->get_query_params();
        
        $args = array(
            'post_type'      => 'prefix_item',
            'posts_per_page' => isset( $params['per_page'] ) ? absint( $params['per_page'] ) : 10,
            'paged'          => isset( $params['page'] ) ? absint( $params['page'] ) : 1,
            'orderby'        => isset( $params['orderby'] ) ? sanitize_key( $params['orderby'] ) : 'date',
            'order'          => isset( $params['order'] ) ? strtoupper( sanitize_key( $params['order'] ) ) : 'DESC',
            'post_status'    => 'publish',
        );
        
        if ( ! empty( $params['search'] ) ) {
            $args['s'] = sanitize_text_field( $params['search'] );
        }
        
        /**
         * Filters REST API query args.
         *
         * @since 1.0.0
         * @param array           $args    Query arguments.
         * @param WP_REST_Request $request Request object.
         */
        $args = apply_filters( 'prefix_rest_items_query_args', $args, $request );
        
        $query = new WP_Query( $args );
        $items = array();
        
        if ( $query->have_posts() ) {
            foreach ( $query->posts as $post ) {
                $data    = $this->prepare_item_for_response( $post, $request );
                $items[] = $this->prepare_response_for_collection( $data );
            }
        }
        
        $response = rest_ensure_response( $items );
        
        // Add pagination headers.
        $total_items = $query->found_posts;
        $max_pages   = ceil( $total_items / absint( $args['posts_per_page'] ) );
        
        $response->header( 'X-WP-Total', $total_items );
        $response->header( 'X-WP-TotalPages', $max_pages );
        
        return $response;
    }

    /**
     * Get single item.
     *
     * @param WP_REST_Request $request Full details about the request.
     * @return WP_REST_Response|WP_Error Response object or error.
     */
    public function get_item( $request ) {
        $id   = absint( $request->get_param( 'id' ) );
        $post = get_post( $id );
        
        if ( ! $post || 'prefix_item' !== $post->post_type ) {
            return new WP_Error(
                'rest_item_not_found',
                __( 'Item not found.', 'prefix-plugin' ),
                array( 'status' => 404 )
            );
        }
        
        $data = $this->prepare_item_for_response( $post, $request );
        
        return rest_ensure_response( $data );
    }

    /**
     * Create item.
     *
     * @param WP_REST_Request $request Full details about the request.
     * @return WP_REST_Response|WP_Error Response object or error.
     */
    public function create_item( $request ) {
        if ( ! empty( $request['id'] ) ) {
            return new WP_Error(
                'rest_item_exists',
                __( 'Cannot create existing item.', 'prefix-plugin' ),
                array( 'status' => 400 )
            );
        }
        
        $prepared_post = $this->prepare_item_for_database( $request );
        
        if ( is_wp_error( $prepared_post ) ) {
            return $prepared_post;
        }
        
        $post_id = wp_insert_post( $prepared_post, true );
        
        if ( is_wp_error( $post_id ) ) {
            return $post_id;
        }
        
        // Save meta data.
        if ( isset( $request['meta'] ) ) {
            $this->update_item_meta( $post_id, $request['meta'] );
        }
        
        $post = get_post( $post_id );
        
        /**
         * Fires after item is created via REST API.
         *
         * @since 1.0.0
         * @param WP_Post         $post    Inserted post object.
         * @param WP_REST_Request $request Request object.
         * @param bool            $creating True when creating, false updating.
         */
        do_action( 'prefix_rest_insert_item', $post, $request, true );
        
        $response = $this->prepare_item_for_response( $post, $request );
        $response = rest_ensure_response( $response );
        
        $response->set_status( 201 );
        $response->header( 'Location', rest_url( sprintf( '%s/%s/%d', $this->namespace, $this->rest_base, $post_id ) ) );
        
        return $response;
    }

    /**
     * Check permission for getting items.
     *
     * @param WP_REST_Request $request Full details about the request.
     * @return bool|WP_Error True if permitted, error otherwise.
     */
    public function get_items_permissions_check( $request ) {
        // Public endpoint.
        return true;
    }

    /**
     * Check permission for creating item.
     *
     * @param WP_REST_Request $request Full details about the request.
     * @return bool|WP_Error True if permitted, error otherwise.
     */
    public function create_item_permissions_check( $request ) {
        if ( ! current_user_can( 'publish_posts' ) ) {
            return new WP_Error(
                'rest_forbidden',
                __( 'Sorry, you cannot create items.', 'prefix-plugin' ),
                array( 'status' => rest_authorization_required_code() )
            );
        }
        return true;
    }

    /**
     * Prepare item for response.
     *
     * @param WP_Post         $post    Post object.
     * @param WP_REST_Request $request Request object.
     * @return WP_REST_Response Response object.
     */
    public function prepare_item_for_response( $post, $request ) {
        $data = array(
            'id'           => $post->ID,
            'title'        => array(
                'raw'      => $post->post_title,
                'rendered' => get_the_title( $post->ID ),
            ),
            'content'      => array(
                'raw'      => $post->post_content,
                'rendered' => apply_filters( 'the_content', $post->post_content ),
            ),
            'excerpt'      => array(
                'raw'      => $post->post_excerpt,
                'rendered' => get_the_excerpt( $post->ID ),
            ),
            'date'         => mysql_to_rfc3339( $post->post_date ),
            'date_gmt'     => mysql_to_rfc3339( $post->post_date_gmt ),
            'modified'     => mysql_to_rfc3339( $post->post_modified ),
            'modified_gmt' => mysql_to_rfc3339( $post->post_modified_gmt ),
            'status'       => $post->post_status,
            'author'       => (int) $post->post_author,
            'featured_media' => (int) get_post_thumbnail_id( $post->ID ),
            'meta'         => $this->get_item_meta( $post->ID ),
        );
        
        $context = ! empty( $request['context'] ) ? $request['context'] : 'view';
        $data    = $this->add_additional_fields_to_object( $data, $request );
        $data    = $this->filter_response_by_context( $data, $context );
        
        $response = rest_ensure_response( $data );
        $response->add_links( $this->prepare_links( $post ) );
        
        /**
         * Filters item response.
         *
         * @since 1.0.0
         * @param WP_REST_Response $response Response object.
         * @param WP_Post          $post     Post object.
         * @param WP_REST_Request  $request  Request object.
         */
        return apply_filters( 'prefix_rest_prepare_item', $response, $post, $request );
    }

    /**
     * Get item schema.
     *
     * @return array Schema array.
     */
    public function get_item_schema() {
        if ( $this->schema ) {
            return $this->add_additional_fields_schema( $this->schema );
        }
        
        $this->schema = array(
            '$schema'    => 'http://json-schema.org/draft-04/schema#',
            'title'      => 'prefix_item',
            'type'       => 'object',
            'properties' => array(
                'id'      => array(
                    'description' => __( 'Unique identifier for the item.', 'prefix-plugin' ),
                    'type'        => 'integer',
                    'context'     => array( 'view', 'edit', 'embed' ),
                    'readonly'    => true,
                ),
                'title'   => array(
                    'description' => __( 'The title for the item.', 'prefix-plugin' ),
                    'type'        => 'object',
                    'context'     => array( 'view', 'edit', 'embed' ),
                    'properties'  => array(
                        'raw'      => array(
                            'description' => __( 'Title, as it exists in the database.', 'prefix-plugin' ),
                            'type'        => 'string',
                            'context'     => array( 'edit' ),
                        ),
                        'rendered' => array(
                            'description' => __( 'HTML title, transformed for display.', 'prefix-plugin' ),
                            'type'        => 'string',
                            'context'     => array( 'view', 'edit', 'embed' ),
                            'readonly'    => true,
                        ),
                    ),
                ),
                'content' => array(
                    'description' => __( 'The content for the item.', 'prefix-plugin' ),
                    'type'        => 'object',
                    'context'     => array( 'view', 'edit' ),
                    'properties'  => array(
                        'raw'      => array(
                            'description' => __( 'Content, as it exists in the database.', 'prefix-plugin' ),
                            'type'        => 'string',
                            'context'     => array( 'edit' ),
                        ),
                        'rendered' => array(
                            'description' => __( 'HTML content, transformed for display.', 'prefix-plugin' ),
                            'type'        => 'string',
                            'context'     => array( 'view', 'edit' ),
                            'readonly'    => true,
                        ),
                    ),
                ),
                'status'  => array(
                    'description' => __( 'A named status for the item.', 'prefix-plugin' ),
                    'type'        => 'string',
                    'enum'        => array( 'publish', 'future', 'draft', 'pending', 'private' ),
                    'context'     => array( 'view', 'edit' ),
                ),
                'date'    => array(
                    'description' => __( "The date the item was published, in the site's timezone.", 'prefix-plugin' ),
                    'type'        => array( 'string', 'null' ),
                    'format'      => 'date-time',
                    'context'     => array( 'view', 'edit', 'embed' ),
                ),
            ),
        );
        
        return $this->add_additional_fields_schema( $this->schema );
    }
}

// Register REST routes.
add_action( 'rest_api_init', function() {
    $controller = new Prefix_REST_Controller();
    $controller->register_routes();
} );
```

---

## Elementor Widget Development

> **Reference**: https://developers.elementor.com/docs/widgets/

### Custom Elementor Widget

```php
<?php
/**
 * Custom Elementor widget.
 *
 * @package Prefix_Elementor
 */

// Exit if accessed directly.
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Class Prefix_Elementor_Widget
 *
 * Custom Elementor widget implementation.
 */
class Prefix_Elementor_Widget extends \Elementor\Widget_Base {

    /**
     * Get widget name.
     *
     * @return string Widget name.
     */
    public function get_name(): string {
        return 'prefix_custom_widget';
    }

    /**
     * Get widget title.
     *
     * @return string Widget title.
     */
    public function get_title(): string {
        return esc_html__( 'Custom Widget', 'prefix-elementor' );
    }

    /**
     * Get widget icon.
     *
     * @return string Widget icon.
     */
    public function get_icon(): string {
        return 'eicon-code';
    }

    /**
     * Get widget categories.
     *
     * @return array Widget categories.
     */
    public function get_categories(): array {
        return array( 'general', 'prefix-widgets' );
    }

    /**
     * Get widget keywords.
     *
     * @return array Widget keywords.
     */
    public function get_keywords(): array {
        return array( 'custom', 'widget', 'prefix' );
    }

    /**
     * Get custom help URL.
     *
     * @return string Widget help URL.
     */
    public function get_custom_help_url(): string {
        return 'https://example.com/docs/custom-widget/';
    }

    /**
     * Get script dependencies.
     *
     * @return array Script dependencies.
     */
    public function get_script_depends(): array {
        return array( 'prefix-widget-scripts' );
    }

    /**
     * Get style dependencies.
     *
     * @return array Style dependencies.
     */
    public function get_style_depends(): array {
        return array( 'prefix-widget-styles' );
    }

    /**
     * Register widget controls.
     *
     * @return void
     */
    protected function register_controls(): void {
        // Content Section.
        $this->start_controls_section(
            'content_section',
            array(
                'label' => esc_html__( 'Content', 'prefix-elementor' ),
                'tab'   => \Elementor\Controls_Manager::TAB_CONTENT,
            )
        );

        $this->add_control(
            'title',
            array(
                'label'       => esc_html__( 'Title', 'prefix-elementor' ),
                'type'        => \Elementor\Controls_Manager::TEXT,
                'default'     => esc_html__( 'Default Title', 'prefix-elementor' ),
                'placeholder' => esc_html__( 'Enter title', 'prefix-elementor' ),
                'label_block' => true,
                'dynamic'     => array(
                    'active' => true,
                ),
            )
        );

        $this->add_control(
            'description',
            array(
                'label'       => esc_html__( 'Description', 'prefix-elementor' ),
                'type'        => \Elementor\Controls_Manager::WYSIWYG,
                'default'     => esc_html__( 'Default description text.', 'prefix-elementor' ),
                'placeholder' => esc_html__( 'Enter description', 'prefix-elementor' ),
                'dynamic'     => array(
                    'active' => true,
                ),
            )
        );

        $this->add_control(
            'image',
            array(
                'label'   => esc_html__( 'Choose Image', 'prefix-elementor' ),
                'type'    => \Elementor\Controls_Manager::MEDIA,
                'default' => array(
                    'url' => \Elementor\Utils::get_placeholder_image_src(),
                ),
                'dynamic' => array(
                    'active' => true,
                ),
            )
        );

        $this->add_group_control(
            \Elementor\Group_Control_Image_Size::get_type(),
            array(
                'name'    => 'image',
                'default' => 'large',
            )
        );

        $this->add_control(
            'link',
            array(
                'label'       => esc_html__( 'Link', 'prefix-elementor' ),
                'type'        => \Elementor\Controls_Manager::URL,
                'placeholder' => esc_html__( 'https://example.com', 'prefix-elementor' ),
                'default'     => array(
                    'url'         => '',
                    'is_external' => true,
                    'nofollow'    => true,
                ),
                'dynamic'     => array(
                    'active' => true,
                ),
            )
        );

        $this->end_controls_section();

        // Style Section.
        $this->start_controls_section(
            'style_section',
            array(
                'label' => esc_html__( 'Style', 'prefix-elementor' ),
                'tab'   => \Elementor\Controls_Manager::TAB_STYLE,
            )
        );

        $this->add_control(
            'title_color',
            array(
                'label'     => esc_html__( 'Title Color', 'prefix-elementor' ),
                'type'      => \Elementor\Controls_Manager::COLOR,
                'default'   => '#333333',
                'selectors' => array(
                    '{{WRAPPER}} .prefix-widget-title' => 'color: {{VALUE}};',
                ),
            )
        );

        $this->add_group_control(
            \Elementor\Group_Control_Typography::get_type(),
            array(
                'name'     => 'title_typography',
                'label'    => esc_html__( 'Title Typography', 'prefix-elementor' ),
                'selector' => '{{WRAPPER}} .prefix-widget-title',
            )
        );

        $this->add_responsive_control(
            'title_margin',
            array(
                'label'      => esc_html__( 'Title Margin', 'prefix-elementor' ),
                'type'       => \Elementor\Controls_Manager::DIMENSIONS,
                'size_units' => array( 'px', 'em', '%' ),
                'selectors'  => array(
                    '{{WRAPPER}} .prefix-widget-title' => 'margin: {{TOP}}{{UNIT}} {{RIGHT}}{{UNIT}} {{BOTTOM}}{{UNIT}} {{LEFT}}{{UNIT}};',
                ),
            )
        );

        $this->add_group_control(
            \Elementor\Group_Control_Box_Shadow::get_type(),
            array(
                'name'     => 'box_shadow',
                'label'    => esc_html__( 'Box Shadow', 'prefix-elementor' ),
                'selector' => '{{WRAPPER}} .prefix-widget-wrapper',
            )
        );

        $this->end_controls_section();
    }

    /**
     * Render widget output on the frontend.
     *
     * @return void
     */
    protected function render(): void {
        $settings = $this->get_settings_for_display();

        // Prepare link attributes.
        if ( ! empty( $settings['link']['url'] ) ) {
            $this->add_link_attributes( 'link', $settings['link'] );
        }

        // Get image HTML.
        $image_html = '';
        if ( ! empty( $settings['image']['url'] ) ) {
            $image_html = \Elementor\Group_Control_Image_Size::get_attachment_image_html( $settings, 'image' );
        }

        ?>
        <div class="prefix-widget-wrapper">
            <?php if ( ! empty( $settings['image']['url'] ) ) : ?>
                <div class="prefix-widget-image">
                    <?php
                    if ( ! empty( $settings['link']['url'] ) ) {
                        echo '<a ' . $this->get_render_attribute_string( 'link' ) . '>';
                    }
                    echo wp_kses_post( $image_html );
                    if ( ! empty( $settings['link']['url'] ) ) {
                        echo '</a>';
                    }
                    ?>
                </div>
            <?php endif; ?>

            <?php if ( ! empty( $settings['title'] ) ) : ?>
                <h3 class="prefix-widget-title">
                    <?php
                    if ( ! empty( $settings['link']['url'] ) ) {
                        echo '<a ' . $this->get_render_attribute_string( 'link' ) . '>';
                    }
                    echo esc_html( $settings['title'] );
                    if ( ! empty( $settings['link']['url'] ) ) {
                        echo '</a>';
                    }
                    ?>
                </h3>
            <?php endif; ?>

            <?php if ( ! empty( $settings['description'] ) ) : ?>
                <div class="prefix-widget-description">
                    <?php echo wp_kses_post( $settings['description'] ); ?>
                </div>
            <?php endif; ?>
        </div>
        <?php
    }

    /**
     * Render widget output in the editor (JavaScript).
     *
     * @return void
     */
    protected function content_template(): void {
        ?>
        <#
        var imageUrl = '';
        if ( settings.image.url ) {
            var image = {
                id: settings.image.id,
                url: settings.image.url,
                size: settings.image_size,
                dimension: settings.image_custom_dimension,
                model: view.getEditModel()
            };
            var image_url = elementor.imagesManager.getImageUrl( image );
            imageUrl = '<img src="' + image_url + '" />';
        }

        var linkStart = '';
        var linkEnd = '';
        if ( settings.link.url ) {
            view.addRenderAttribute( 'link', 'href', settings.link.url );
            if ( settings.link.is_external ) {
                view.addRenderAttribute( 'link', 'target', '_blank' );
            }
            if ( settings.link.nofollow ) {
                view.addRenderAttribute( 'link', 'rel', 'nofollow' );
            }
            linkStart = '<a ' + view.getRenderAttributeString( 'link' ) + '>';
            linkEnd = '</a>';
        }
        #>
        <div class="prefix-widget-wrapper">
            <# if ( settings.image.url ) { #>
                <div class="prefix-widget-image">
                    {{{ linkStart }}}{{{ imageUrl }}}{{{ linkEnd }}}
                </div>
            <# } #>

            <# if ( settings.title ) { #>
                <h3 class="prefix-widget-title">
                    {{{ linkStart }}}{{{ settings.title }}}{{{ linkEnd }}}
                </h3>
            <# } #>

            <# if ( settings.description ) { #>
                <div class="prefix-widget-description">
                    {{{ settings.description }}}
                </div>
            <# } #>
        </div>
        <?php
    }
}

/**
 * Register Elementor widget.
 *
 * @param \Elementor\Widgets_Manager $widgets_manager Elementor widgets manager.
 * @return void
 */
function prefix_register_elementor_widgets( $widgets_manager ) {
    $widgets_manager->register( new Prefix_Elementor_Widget() );
}
add_action( 'elementor/widgets/register', 'prefix_register_elementor_widgets' );

/**
 * Register Elementor widget category.
 *
 * @param \Elementor\Elements_Manager $elements_manager Elementor elements manager.
 * @return void
 */
function prefix_register_elementor_categories( $elements_manager ) {
    $elements_manager->add_category(
        'prefix-widgets',
        array(
            'title' => esc_html__( 'Prefix Widgets', 'prefix-elementor' ),
            'icon'  => 'fa fa-plug',
        )
    );
}
add_action( 'elementor/elements/categories_registered', 'prefix_register_elementor_categories' );
```

---

## JetEngine & Crocoblock Development

> **Reference**: https://crocoblock.com/knowledge-base/plugins/jetengine/

### JetEngine Custom Callback

```php
<?php
/**
 * JetEngine custom callbacks and integrations.
 *
 * @package Prefix_JetEngine
 */

// Exit if accessed directly.
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Add custom callback to JetEngine.
 *
 * @param array $callbacks Existing callbacks.
 * @return array Modified callbacks.
 */
function prefix_jetengine_add_custom_callback( $callbacks ) {
    $callbacks['prefix_custom_format'] = array(
        'label' => __( 'Prefix Custom Format', 'prefix-jetengine' ),
    );
    
    return $callbacks;
}
add_filter( 'jet-engine/listings/allowed-callbacks', 'prefix_jetengine_add_custom_callback' );

/**
 * Process custom callback.
 *
 * @param mixed  $result     Current result.
 * @param string $callback   Callback name.
 * @param array  $settings   Widget settings.
 * @param object $widget     Widget instance.
 * @return mixed Processed result.
 */
function prefix_jetengine_process_callback( $result, $callback, $settings, $widget ) {
    if ( 'prefix_custom_format' !== $callback ) {
        return $result;
    }
    
    // Custom processing logic.
    if ( is_numeric( $result ) ) {
        return number_format_i18n( $result, 2 );
    }
    
    return $result;
}
add_filter( 'jet-engine/listings/allowed-callbacks-args', 'prefix_jetengine_process_callback', 10, 4 );

/**
 * Register custom JetEngine macro.
 *
 * @return void
 */
function prefix_jetengine_register_macros() {
    if ( ! class_exists( 'Jet_Engine_Base_Macros' ) ) {
        return;
    }
    
    /**
     * Custom macro class.
     */
    class Prefix_JetEngine_Custom_Macro extends Jet_Engine_Base_Macros {
        
        /**
         * Get macro ID.
         *
         * @return string
         */
        public function macros_tag() {
            return 'prefix_custom_data';
        }
        
        /**
         * Get macro name.
         *
         * @return string
         */
        public function macros_name() {
            return __( 'Prefix Custom Data', 'prefix-jetengine' );
        }
        
        /**
         * Get macro arguments.
         *
         * @return array
         */
        public function macros_args() {
            return array(
                'field_key' => array(
                    'label'   => __( 'Field Key', 'prefix-jetengine' ),
                    'type'    => 'text',
                    'default' => '',
                ),
                'fallback' => array(
                    'label'   => __( 'Fallback Value', 'prefix-jetengine' ),
                    'type'    => 'text',
                    'default' => '',
                ),
            );
        }
        
        /**
         * Process macro.
         *
         * @param mixed $result Default result.
         * @param array $args   Macro arguments.
         * @return mixed Processed result.
         */
        public function macros_callback( $result = null, $args = array() ) {
            $field_key = ! empty( $args['field_key'] ) ? $args['field_key'] : '';
            $fallback  = ! empty( $args['fallback'] ) ? $args['fallback'] : '';
            
            if ( empty( $field_key ) ) {
                return $fallback;
            }
            
            // Get current object.
            $object_id = jet_engine()->listings->data->get_current_object_id();
            
            if ( ! $object_id ) {
                return $fallback;
            }
            
            // Get meta value.
            $value = get_post_meta( $object_id, $field_key, true );
            
            if ( empty( $value ) ) {
                return $fallback;
            }
            
            /**
             * Filters custom macro value.
             *
             * @since 1.0.0
             * @param mixed  $value     Meta value.
             * @param int    $object_id Object ID.
             * @param string $field_key Field key.
             */
            return apply_filters( 'prefix_jetengine_custom_macro_value', $value, $object_id, $field_key );
        }
    }
    
    // Register macro.
    new Prefix_JetEngine_Custom_Macro();
}
add_action( 'jet-engine/register-macros', 'prefix_jetengine_register_macros' );

/**
 * Add custom Query Builder query type.
 *
 * @return void
 */
function prefix_jetengine_register_query_type() {
    if ( ! class_exists( 'Jet_Engine_Base_Query' ) ) {
        return;
    }
    
    /**
     * Custom query class.
     */
    class Prefix_JetEngine_Custom_Query extends Jet_Engine_Base_Query {
        
        /**
         * Get query type ID.
         *
         * @return string
         */
        public function get_id() {
            return 'prefix-custom-query';
        }
        
        /**
         * Get query type name.
         *
         * @return string
         */
        public function get_name() {
            return __( 'Prefix Custom Query', 'prefix-jetengine' );
        }
        
        /**
         * Get query items.
         *
         * @return array
         */
        public function get_items() {
            $args = $this->final_query;
            
            // Custom query logic here.
            global $wpdb;
            
            $results = $wpdb->get_results(
                $wpdb->prepare(
                    "SELECT * FROM {$wpdb->prefix}prefix_custom_table WHERE status = %s LIMIT %d",
                    isset( $args['status'] ) ? $args['status'] : 'active',
                    isset( $args['limit'] ) ? absint( $args['limit'] ) : 10
                )
            );
            
            return $results ? $results : array();
        }
        
        /**
         * Get total items count.
         *
         * @return int
         */
        public function get_items_total_count() {
            global $wpdb;
            
            $count = $wpdb->get_var(
                "SELECT COUNT(*) FROM {$wpdb->prefix}prefix_custom_table WHERE status = 'active'"
            );
            
            return $count ? absint( $count ) : 0;
        }
    }
    
    // Register query type.
    jet_engine()->query_builder->query_types->register_query_type( new Prefix_JetEngine_Custom_Query() );
}
add_action( 'jet-engine/query-builder/query-types/register', 'prefix_jetengine_register_query_type' );
```

---

## JetFormBuilder Development

> **Reference**: https://jetformbuilder.com/

### JetFormBuilder Custom Action

```php
<?php
/**
 * JetFormBuilder custom actions.
 *
 * @package Prefix_JetFormBuilder
 */

// Exit if accessed directly.
if ( ! defined( 'ABSPATH' ) ) {
    exit;
}

/**
 * Custom hook action for JetFormBuilder.
 *
 * @param array $request Form request data.
 * @param object $action_handler Action handler instance.
 * @return void
 */
function prefix_jetformbuilder_custom_action( $request, $action_handler ) {
    // Validate request data.
    if ( empty( $request['email'] ) ) {
        throw new \Jet_Form_Builder\Exceptions\Action_Exception(
            'empty_field',
            array( 'email' )
        );
    }
    
    // Get form field values.
    $email   = sanitize_email( $request['email'] );
    $name    = isset( $request['name'] ) ? sanitize_text_field( $request['name'] ) : '';
    $message = isset( $request['message'] ) ? sanitize_textarea_field( $request['message'] ) : '';
    
    // Process the data.
    $result = prefix_process_form_data( array(
        'email'   => $email,
        'name'    => $name,
        'message' => $message,
    ) );
    
    if ( is_wp_error( $result ) ) {
        throw ( new \Jet_Form_Builder\Exceptions\Action_Exception( $result->get_error_message() ) )->dynamic_error();
    }
    
    // Update request context if needed.
    jet_fb_context()->update_request( $result['id'], 'created_id' );
    
    /**
     * Fires after custom form action is processed.
     *
     * @since 1.0.0
     * @param array $request Form request data.
     * @param mixed $result  Processing result.
     */
    do_action( 'prefix_jetformbuilder_after_custom_action', $request, $result );
}
add_action( 'jet-form-builder/custom-action/prefix_custom_action', 'prefix_jetformbuilder_custom_action', 10, 2 );

/**
 * Custom form validation.
 *
 * @param bool   $is_valid Current validation state.
 * @param string $value    Field value.
 * @param array  $args     Validation arguments.
 * @param object $handler  Handler instance.
 * @return bool|WP_Error Validation result.
 */
function prefix_jetformbuilder_custom_validation( $is_valid, $value, $args, $handler ) {
    // Custom validation logic.
    if ( empty( $value ) ) {
        return true; // Skip if empty (required validation handles this).
    }
    
    // Example: Validate custom format.
    if ( ! preg_match( '/^[A-Z]{2}[0-9]{6}$/', $value ) ) {
        return new WP_Error(
            'invalid_format',
            __( 'Please enter a valid code (2 letters followed by 6 numbers).', 'prefix-jetformbuilder' )
        );
    }
    
    return $is_valid;
}
add_filter( 'jet-form-builder/validate-field/prefix_custom_format', 'prefix_jetformbuilder_custom_validation', 10, 4 );

/**
 * Register custom form field type.
 *
 * @return void
 */
function prefix_jetformbuilder_register_field() {
    if ( ! class_exists( 'Jet_Form_Builder\Blocks\Types\Base' ) ) {
        return;
    }
    
    /**
     * Custom field block.
     */
    class Prefix_JFB_Custom_Field extends \Jet_Form_Builder\Blocks\Types\Base {
        
        /**
         * Get block name.
         *
         * @return string
         */
        public function get_name() {
            return 'prefix-custom-field';
        }
        
        /**
         * Get block title.
         *
         * @return string
         */
        public function get_title() {
            return __( 'Prefix Custom Field', 'prefix-jetformbuilder' );
        }
        
        /**
         * Get block icon.
         *
         * @return string
         */
        public function get_icon() {
            return '<svg>...</svg>';
        }
        
        /**
         * Get block render.
         *
         * @param array $attributes Block attributes.
         * @return string Rendered HTML.
         */
        public function get_block_render( $attributes ) {
            $name        = $this->block_attrs['name'] ?? '';
            $placeholder = $this->block_attrs['placeholder'] ?? '';
            $required    = $this->block_attrs['required'] ?? false;
            
            ob_start();
            ?>
            <div class="jet-form-builder__field prefix-custom-field">
                <input 
                    type="text" 
                    name="<?php echo esc_attr( $name ); ?>"
                    placeholder="<?php echo esc_attr( $placeholder ); ?>"
                    class="jet-form-builder__field-input"
                    <?php echo $required ? 'required' : ''; ?>
                    data-field-type="prefix-custom-field"
                >
            </div>
            <?php
            return ob_get_clean();
        }
    }
}
add_action( 'jet-form-builder/blocks/register', 'prefix_jetformbuilder_register_field' );
```

---

## Code Review Checklist

### Pre-Submission Checklist

```markdown
## WordPress Code Review Checklist

### Security
- [ ] All user input is sanitized
- [ ] All output is properly escaped
- [ ] Nonces are used for all forms and AJAX
- [ ] Capability checks are in place
- [ ] Prepared statements for all database queries
- [ ] No direct file access without ABSPATH check
- [ ] No `eval()` or `create_function()`
- [ ] File uploads are validated

### Coding Standards
- [ ] Follows WordPress PHP Coding Standards
- [ ] Follows WordPress JavaScript Coding Standards
- [ ] Follows WordPress CSS Coding Standards
- [ ] No PHP errors, warnings, or notices
- [ ] No JavaScript console errors
- [ ] Passed PHPCS with WordPress ruleset

### Performance
- [ ] Database queries are optimized
- [ ] Proper use of transients/caching
- [ ] Assets are minified for production
- [ ] No unnecessary database calls in loops
- [ ] Lazy loading implemented where appropriate
- [ ] No blocking resources

### Internationalization
- [ ] All strings are translatable
- [ ] Text domain is consistent
- [ ] Proper translator comments
- [ ] POT file is generated and up-to-date

### Accessibility
- [ ] Semantic HTML is used
- [ ] All images have alt text
- [ ] Forms have proper labels
- [ ] Color contrast meets WCAG AA
- [ ] Keyboard navigation works
- [ ] Screen reader compatible

### Documentation
- [ ] All functions have PHPDoc blocks
- [ ] README.txt is complete and valid
- [ ] CHANGELOG.md is updated
- [ ] Inline comments are meaningful

### WordPress Integration
- [ ] Uses WordPress APIs properly
- [ ] Hooks are properly documented
- [ ] No conflicts with other plugins
- [ ] Graceful degradation if dependencies missing
- [ ] Uninstall routine cleans up properly

### WooCommerce (if applicable)
- [ ] HPOS compatibility declared
- [ ] Cart/Checkout Blocks compatibility
- [ ] Follows WooCommerce coding standards
- [ ] Template overrides are documented
- [ ] Hooks follow WooCommerce conventions
```

---

## Quick Reference Commands

```bash
# WordPress Coding Standards check
composer require --dev wp-coding-standards/wpcs
./vendor/bin/phpcs --standard=WordPress /path/to/plugin

# Auto-fix issues
./vendor/bin/phpcbf --standard=WordPress /path/to/plugin

# Generate POT file
wp i18n make-pot /path/to/plugin /path/to/plugin/languages/plugin-name.pot

# Create block
npx @wordpress/create-block prefix-custom-block

# Build block assets
npm run build

# Run PHPUnit tests
./vendor/bin/phpunit

# Check JavaScript
npx eslint assets/js/

# Minify CSS
npx postcss assets/css/style.css -o assets/css/style.min.css

# Minify JavaScript
npx terser assets/js/script.js -o assets/js/script.min.js
```

---

## Custom Post Types & Taxonomies

> **Reference**: https://developer.wordpress.org/plugins/post-types/

### Registering Custom Post Types

```php
<?php
/**
 * Register custom post types.
 *
 * @package Prefix_Plugin
 */

/**
 * Register the 'product' custom post type.
 *
 * @return void
 */
function prefix_register_post_types() {
    
    $labels = array(
        'name'                  => _x( 'Products', 'Post type general name', 'textdomain' ),
        'singular_name'         => _x( 'Product', 'Post type singular name', 'textdomain' ),
        'menu_name'             => _x( 'Products', 'Admin Menu text', 'textdomain' ),
        'name_admin_bar'        => _x( 'Product', 'Add New on Toolbar', 'textdomain' ),
        'add_new'               => __( 'Add New', 'textdomain' ),
        'add_new_item'          => __( 'Add New Product', 'textdomain' ),
        'new_item'              => __( 'New Product', 'textdomain' ),
        'edit_item'             => __( 'Edit Product', 'textdomain' ),
        'view_item'             => __( 'View Product', 'textdomain' ),
        'all_items'             => __( 'All Products', 'textdomain' ),
        'search_items'          => __( 'Search Products', 'textdomain' ),
        'parent_item_colon'     => __( 'Parent Products:', 'textdomain' ),
        'not_found'             => __( 'No products found.', 'textdomain' ),
        'not_found_in_trash'    => __( 'No products found in Trash.', 'textdomain' ),
        'featured_image'        => _x( 'Product Cover Image', 'Overrides the "Featured Image" phrase', 'textdomain' ),
        'set_featured_image'    => _x( 'Set cover image', 'Overrides "Set featured image"', 'textdomain' ),
        'remove_featured_image' => _x( 'Remove cover image', 'Overrides "Remove featured image"', 'textdomain' ),
        'use_featured_image'    => _x( 'Use as cover image', 'Overrides "Use as featured image"', 'textdomain' ),
        'archives'              => _x( 'Product archives', 'The post type archive label', 'textdomain' ),
        'insert_into_item'      => _x( 'Insert into product', 'Overrides "Insert into post"', 'textdomain' ),
        'uploaded_to_this_item' => _x( 'Uploaded to this product', 'Overrides "Uploaded to this post"', 'textdomain' ),
        'filter_items_list'     => _x( 'Filter products list', 'Screen reader text', 'textdomain' ),
        'items_list_navigation' => _x( 'Products list navigation', 'Screen reader text', 'textdomain' ),
        'items_list'            => _x( 'Products list', 'Screen reader text', 'textdomain' ),
    );

    $args = array(
        'labels'             => $labels,
        'public'             => true,
        'publicly_queryable' => true,
        'show_ui'            => true,
        'show_in_menu'       => true,
        'query_var'          => true,
        'rewrite'            => array( 'slug' => 'products', 'with_front' => false ),
        'capability_type'    => 'post',
        'has_archive'        => true,
        'hierarchical'       => false,
        'menu_position'      => 20,
        'menu_icon'          => 'dashicons-cart',
        'supports'           => array( 'title', 'editor', 'author', 'thumbnail', 'excerpt', 'comments', 'revisions', 'custom-fields' ),
        'show_in_rest'       => true, // Required for Gutenberg block editor
        'rest_base'          => 'products',
        'rest_controller_class' => 'WP_REST_Posts_Controller',
        'taxonomies'         => array( 'prefix_product_category', 'prefix_product_tag' ),
        'template'           => array(), // Block editor template
        'template_lock'      => false,
    );

    register_post_type( 'prefix_product', $args );
}
add_action( 'init', 'prefix_register_post_types' );
```

### Registering Custom Taxonomies

```php
<?php
/**
 * Register custom taxonomies.
 *
 * @return void
 */
function prefix_register_taxonomies() {
    
    // Hierarchical taxonomy (like categories).
    $category_labels = array(
        'name'                       => _x( 'Product Categories', 'taxonomy general name', 'textdomain' ),
        'singular_name'              => _x( 'Product Category', 'taxonomy singular name', 'textdomain' ),
        'search_items'               => __( 'Search Categories', 'textdomain' ),
        'popular_items'              => __( 'Popular Categories', 'textdomain' ),
        'all_items'                  => __( 'All Categories', 'textdomain' ),
        'parent_item'                => __( 'Parent Category', 'textdomain' ),
        'parent_item_colon'          => __( 'Parent Category:', 'textdomain' ),
        'edit_item'                  => __( 'Edit Category', 'textdomain' ),
        'view_item'                  => __( 'View Category', 'textdomain' ),
        'update_item'                => __( 'Update Category', 'textdomain' ),
        'add_new_item'               => __( 'Add New Category', 'textdomain' ),
        'new_item_name'              => __( 'New Category Name', 'textdomain' ),
        'separate_items_with_commas' => __( 'Separate categories with commas', 'textdomain' ),
        'add_or_remove_items'        => __( 'Add or remove categories', 'textdomain' ),
        'choose_from_most_used'      => __( 'Choose from the most used categories', 'textdomain' ),
        'not_found'                  => __( 'No categories found.', 'textdomain' ),
        'no_terms'                   => __( 'No categories', 'textdomain' ),
        'items_list_navigation'      => __( 'Categories list navigation', 'textdomain' ),
        'items_list'                 => __( 'Categories list', 'textdomain' ),
        'back_to_items'              => __( '&larr; Back to Categories', 'textdomain' ),
    );

    $category_args = array(
        'labels'            => $category_labels,
        'hierarchical'      => true,
        'public'            => true,
        'show_ui'           => true,
        'show_admin_column' => true,
        'show_in_nav_menus' => true,
        'show_tagcloud'     => true,
        'show_in_rest'      => true, // Required for Gutenberg
        'rest_base'         => 'product-categories',
        'rewrite'           => array( 'slug' => 'product-category', 'with_front' => false, 'hierarchical' => true ),
        'query_var'         => true,
    );

    register_taxonomy( 'prefix_product_category', array( 'prefix_product' ), $category_args );

    // Non-hierarchical taxonomy (like tags).
    $tag_labels = array(
        'name'                       => _x( 'Product Tags', 'taxonomy general name', 'textdomain' ),
        'singular_name'              => _x( 'Product Tag', 'taxonomy singular name', 'textdomain' ),
        'search_items'               => __( 'Search Tags', 'textdomain' ),
        'popular_items'              => __( 'Popular Tags', 'textdomain' ),
        'all_items'                  => __( 'All Tags', 'textdomain' ),
        'edit_item'                  => __( 'Edit Tag', 'textdomain' ),
        'view_item'                  => __( 'View Tag', 'textdomain' ),
        'update_item'                => __( 'Update Tag', 'textdomain' ),
        'add_new_item'               => __( 'Add New Tag', 'textdomain' ),
        'new_item_name'              => __( 'New Tag Name', 'textdomain' ),
        'separate_items_with_commas' => __( 'Separate tags with commas', 'textdomain' ),
        'add_or_remove_items'        => __( 'Add or remove tags', 'textdomain' ),
        'choose_from_most_used'      => __( 'Choose from the most used tags', 'textdomain' ),
        'not_found'                  => __( 'No tags found.', 'textdomain' ),
        'back_to_items'              => __( '&larr; Back to Tags', 'textdomain' ),
    );

    $tag_args = array(
        'labels'                => $tag_labels,
        'hierarchical'          => false,
        'public'                => true,
        'show_ui'               => true,
        'show_admin_column'     => true,
        'show_in_nav_menus'     => true,
        'show_tagcloud'         => true,
        'show_in_rest'          => true,
        'rewrite'               => array( 'slug' => 'product-tag', 'with_front' => false ),
        'query_var'             => true,
        'update_count_callback' => '_update_post_term_count', // Important for tag-like behavior
    );

    register_taxonomy( 'prefix_product_tag', array( 'prefix_product' ), $tag_args );
}
// Register taxonomies BEFORE post types or use priority.
add_action( 'init', 'prefix_register_taxonomies', 0 );
```

### Custom Post Type Template Files

```php
// Template Hierarchy for Custom Post Types:
// Single: single-{post_type}.php → single.php → singular.php → index.php
// Archive: archive-{post_type}.php → archive.php → index.php

// For taxonomy archives:
// taxonomy-{taxonomy}-{term}.php → taxonomy-{taxonomy}.php → taxonomy.php → archive.php → index.php
```

### Querying Custom Post Types

```php
<?php
// WP_Query for custom post types.
$args = array(
    'post_type'      => 'prefix_product',
    'posts_per_page' => 10,
    'post_status'    => 'publish',
    'orderby'        => 'date',
    'order'          => 'DESC',
    'tax_query'      => array(
        array(
            'taxonomy' => 'prefix_product_category',
            'field'    => 'slug',
            'terms'    => 'featured',
        ),
    ),
    'meta_query'     => array(
        array(
            'key'     => '_prefix_price',
            'value'   => 100,
            'compare' => '>=',
            'type'    => 'NUMERIC',
        ),
    ),
);

$products = new WP_Query( $args );

if ( $products->have_posts() ) {
    while ( $products->have_posts() ) {
        $products->the_post();
        // Output content.
    }
    wp_reset_postdata(); // Always reset after custom query.
}

// Get terms for a post.
$terms = get_the_terms( get_the_ID(), 'prefix_product_category' );
if ( $terms && ! is_wp_error( $terms ) ) {
    foreach ( $terms as $term ) {
        echo esc_html( $term->name );
    }
}
```

### Flushing Rewrite Rules

```php
<?php
/**
 * Flush rewrite rules on plugin activation.
 *
 * @return void
 */
function prefix_activate() {
    prefix_register_post_types();
    prefix_register_taxonomies();
    flush_rewrite_rules();
}
register_activation_hook( __FILE__, 'prefix_activate' );

/**
 * Flush rewrite rules on plugin deactivation.
 *
 * @return void
 */
function prefix_deactivate() {
    flush_rewrite_rules();
}
register_deactivation_hook( __FILE__, 'prefix_deactivate' );

// NEVER flush rewrite rules on every page load - only on activation/deactivation!
```

---

## Settings API & Admin Menus

> **Reference**: https://developer.wordpress.org/plugins/settings/

### Creating Admin Menu Pages

```php
<?php
/**
 * Register admin menu pages.
 *
 * @return void
 */
function prefix_add_admin_menu() {
    // Top-level menu page.
    add_menu_page(
        __( 'Plugin Settings', 'textdomain' ),     // Page title.
        __( 'My Plugin', 'textdomain' ),           // Menu title.
        'manage_options',                           // Capability required.
        'prefix-settings',                          // Menu slug.
        'prefix_settings_page_html',                // Callback function.
        'dashicons-admin-settings',                 // Icon (dashicon or URL).
        80                                          // Position.
    );

    // Sub-menu page under top-level menu.
    add_submenu_page(
        'prefix-settings',                          // Parent slug.
        __( 'General Settings', 'textdomain' ),    // Page title.
        __( 'General', 'textdomain' ),             // Menu title.
        'manage_options',                           // Capability.
        'prefix-settings',                          // Menu slug (same as parent for first item).
        'prefix_settings_page_html'                 // Callback.
    );

    // Additional sub-menu.
    add_submenu_page(
        'prefix-settings',
        __( 'Advanced Settings', 'textdomain' ),
        __( 'Advanced', 'textdomain' ),
        'manage_options',
        'prefix-advanced-settings',
        'prefix_advanced_settings_page_html'
    );

    // Settings page under WordPress "Settings" menu.
    add_options_page(
        __( 'Plugin Options', 'textdomain' ),      // Page title.
        __( 'My Plugin', 'textdomain' ),           // Menu title.
        'manage_options',                           // Capability.
        'prefix-options',                           // Menu slug.
        'prefix_options_page_html'                  // Callback.
    );
}
add_action( 'admin_menu', 'prefix_add_admin_menu' );
```

### Complete Settings API Implementation

```php
<?php
/**
 * Settings API implementation.
 *
 * @package Prefix_Plugin
 */

/**
 * Register plugin settings using Settings API.
 *
 * @return void
 */
function prefix_register_settings() {
    // Register a setting group.
    register_setting(
        'prefix_settings_group',           // Option group.
        'prefix_settings',                 // Option name (stored in wp_options).
        array(
            'type'              => 'array',
            'sanitize_callback' => 'prefix_sanitize_settings',
            'default'           => prefix_get_default_settings(),
        )
    );

    // Add settings section.
    add_settings_section(
        'prefix_general_section',          // Section ID.
        __( 'General Settings', 'textdomain' ), // Section title.
        'prefix_general_section_callback', // Callback for section description.
        'prefix-settings'                  // Page slug.
    );

    // Add settings fields.
    add_settings_field(
        'prefix_enable_feature',           // Field ID.
        __( 'Enable Feature', 'textdomain' ), // Field title.
        'prefix_checkbox_field_callback',  // Callback to render field.
        'prefix-settings',                 // Page slug.
        'prefix_general_section',          // Section ID.
        array(                             // Additional arguments.
            'label_for'   => 'prefix_enable_feature',
            'option_name' => 'prefix_settings',
            'field_name'  => 'enable_feature',
            'description' => __( 'Enable the main feature of this plugin.', 'textdomain' ),
        )
    );

    add_settings_field(
        'prefix_api_key',
        __( 'API Key', 'textdomain' ),
        'prefix_text_field_callback',
        'prefix-settings',
        'prefix_general_section',
        array(
            'label_for'   => 'prefix_api_key',
            'option_name' => 'prefix_settings',
            'field_name'  => 'api_key',
            'type'        => 'password',
            'description' => __( 'Enter your API key.', 'textdomain' ),
        )
    );

    add_settings_field(
        'prefix_items_per_page',
        __( 'Items Per Page', 'textdomain' ),
        'prefix_number_field_callback',
        'prefix-settings',
        'prefix_general_section',
        array(
            'label_for'   => 'prefix_items_per_page',
            'option_name' => 'prefix_settings',
            'field_name'  => 'items_per_page',
            'min'         => 1,
            'max'         => 100,
            'step'        => 1,
            'description' => __( 'Number of items to display per page.', 'textdomain' ),
        )
    );

    add_settings_field(
        'prefix_display_mode',
        __( 'Display Mode', 'textdomain' ),
        'prefix_select_field_callback',
        'prefix-settings',
        'prefix_general_section',
        array(
            'label_for'   => 'prefix_display_mode',
            'option_name' => 'prefix_settings',
            'field_name'  => 'display_mode',
            'options'     => array(
                'grid' => __( 'Grid', 'textdomain' ),
                'list' => __( 'List', 'textdomain' ),
                'card' => __( 'Card', 'textdomain' ),
            ),
            'description' => __( 'Choose how items are displayed.', 'textdomain' ),
        )
    );

    add_settings_field(
        'prefix_custom_css',
        __( 'Custom CSS', 'textdomain' ),
        'prefix_textarea_field_callback',
        'prefix-settings',
        'prefix_general_section',
        array(
            'label_for'   => 'prefix_custom_css',
            'option_name' => 'prefix_settings',
            'field_name'  => 'custom_css',
            'rows'        => 5,
            'description' => __( 'Add custom CSS styles.', 'textdomain' ),
        )
    );
}
add_action( 'admin_init', 'prefix_register_settings' );

/**
 * Get default settings.
 *
 * @return array Default settings.
 */
function prefix_get_default_settings() {
    return array(
        'enable_feature' => false,
        'api_key'        => '',
        'items_per_page' => 10,
        'display_mode'   => 'grid',
        'custom_css'     => '',
    );
}

/**
 * Sanitize settings.
 *
 * @param array $input Raw input data.
 * @return array Sanitized data.
 */
function prefix_sanitize_settings( $input ) {
    $sanitized = array();
    $defaults  = prefix_get_default_settings();

    // Checkbox (boolean).
    $sanitized['enable_feature'] = isset( $input['enable_feature'] ) ? true : false;

    // Text field.
    $sanitized['api_key'] = isset( $input['api_key'] ) 
        ? sanitize_text_field( $input['api_key'] ) 
        : $defaults['api_key'];

    // Number field.
    $sanitized['items_per_page'] = isset( $input['items_per_page'] ) 
        ? absint( $input['items_per_page'] ) 
        : $defaults['items_per_page'];

    // Ensure within range.
    if ( $sanitized['items_per_page'] < 1 || $sanitized['items_per_page'] > 100 ) {
        $sanitized['items_per_page'] = $defaults['items_per_page'];
    }

    // Select field.
    $valid_modes = array( 'grid', 'list', 'card' );
    $sanitized['display_mode'] = isset( $input['display_mode'] ) && in_array( $input['display_mode'], $valid_modes, true )
        ? $input['display_mode']
        : $defaults['display_mode'];

    // Textarea (CSS).
    $sanitized['custom_css'] = isset( $input['custom_css'] ) 
        ? wp_strip_all_tags( $input['custom_css'] ) 
        : $defaults['custom_css'];

    return $sanitized;
}

/**
 * Section callback.
 *
 * @param array $args Section arguments.
 * @return void
 */
function prefix_general_section_callback( $args ) {
    ?>
    <p><?php esc_html_e( 'Configure the general settings for the plugin.', 'textdomain' ); ?></p>
    <?php
}

/**
 * Checkbox field callback.
 *
 * @param array $args Field arguments.
 * @return void
 */
function prefix_checkbox_field_callback( $args ) {
    $options = get_option( $args['option_name'], prefix_get_default_settings() );
    $value   = isset( $options[ $args['field_name'] ] ) ? $options[ $args['field_name'] ] : false;
    ?>
    <input 
        type="checkbox" 
        id="<?php echo esc_attr( $args['label_for'] ); ?>" 
        name="<?php echo esc_attr( $args['option_name'] . '[' . $args['field_name'] . ']' ); ?>" 
        value="1" 
        <?php checked( $value, true ); ?>
    />
    <?php if ( ! empty( $args['description'] ) ) : ?>
        <p class="description"><?php echo esc_html( $args['description'] ); ?></p>
    <?php endif; ?>
    <?php
}

/**
 * Text field callback.
 *
 * @param array $args Field arguments.
 * @return void
 */
function prefix_text_field_callback( $args ) {
    $options = get_option( $args['option_name'], prefix_get_default_settings() );
    $value   = isset( $options[ $args['field_name'] ] ) ? $options[ $args['field_name'] ] : '';
    $type    = isset( $args['type'] ) ? $args['type'] : 'text';
    ?>
    <input 
        type="<?php echo esc_attr( $type ); ?>" 
        id="<?php echo esc_attr( $args['label_for'] ); ?>" 
        name="<?php echo esc_attr( $args['option_name'] . '[' . $args['field_name'] . ']' ); ?>" 
        value="<?php echo esc_attr( $value ); ?>" 
        class="regular-text"
    />
    <?php if ( ! empty( $args['description'] ) ) : ?>
        <p class="description"><?php echo esc_html( $args['description'] ); ?></p>
    <?php endif; ?>
    <?php
}

/**
 * Number field callback.
 *
 * @param array $args Field arguments.
 * @return void
 */
function prefix_number_field_callback( $args ) {
    $options = get_option( $args['option_name'], prefix_get_default_settings() );
    $value   = isset( $options[ $args['field_name'] ] ) ? $options[ $args['field_name'] ] : '';
    ?>
    <input 
        type="number" 
        id="<?php echo esc_attr( $args['label_for'] ); ?>" 
        name="<?php echo esc_attr( $args['option_name'] . '[' . $args['field_name'] . ']' ); ?>" 
        value="<?php echo esc_attr( $value ); ?>" 
        min="<?php echo esc_attr( $args['min'] ?? 0 ); ?>"
        max="<?php echo esc_attr( $args['max'] ?? '' ); ?>"
        step="<?php echo esc_attr( $args['step'] ?? 1 ); ?>"
        class="small-text"
    />
    <?php if ( ! empty( $args['description'] ) ) : ?>
        <p class="description"><?php echo esc_html( $args['description'] ); ?></p>
    <?php endif; ?>
    <?php
}

/**
 * Select field callback.
 *
 * @param array $args Field arguments.
 * @return void
 */
function prefix_select_field_callback( $args ) {
    $options      = get_option( $args['option_name'], prefix_get_default_settings() );
    $value        = isset( $options[ $args['field_name'] ] ) ? $options[ $args['field_name'] ] : '';
    $select_options = isset( $args['options'] ) ? $args['options'] : array();
    ?>
    <select 
        id="<?php echo esc_attr( $args['label_for'] ); ?>" 
        name="<?php echo esc_attr( $args['option_name'] . '[' . $args['field_name'] . ']' ); ?>"
    >
        <?php foreach ( $select_options as $key => $label ) : ?>
            <option value="<?php echo esc_attr( $key ); ?>" <?php selected( $value, $key ); ?>>
                <?php echo esc_html( $label ); ?>
            </option>
        <?php endforeach; ?>
    </select>
    <?php if ( ! empty( $args['description'] ) ) : ?>
        <p class="description"><?php echo esc_html( $args['description'] ); ?></p>
    <?php endif; ?>
    <?php
}

/**
 * Textarea field callback.
 *
 * @param array $args Field arguments.
 * @return void
 */
function prefix_textarea_field_callback( $args ) {
    $options = get_option( $args['option_name'], prefix_get_default_settings() );
    $value   = isset( $options[ $args['field_name'] ] ) ? $options[ $args['field_name'] ] : '';
    $rows    = isset( $args['rows'] ) ? $args['rows'] : 5;
    ?>
    <textarea 
        id="<?php echo esc_attr( $args['label_for'] ); ?>" 
        name="<?php echo esc_attr( $args['option_name'] . '[' . $args['field_name'] . ']' ); ?>" 
        rows="<?php echo esc_attr( $rows ); ?>"
        class="large-text code"
    ><?php echo esc_textarea( $value ); ?></textarea>
    <?php if ( ! empty( $args['description'] ) ) : ?>
        <p class="description"><?php echo esc_html( $args['description'] ); ?></p>
    <?php endif; ?>
    <?php
}

/**
 * Settings page HTML.
 *
 * @return void
 */
function prefix_settings_page_html() {
    // Check user capabilities.
    if ( ! current_user_can( 'manage_options' ) ) {
        return;
    }

    // Add settings saved message.
    if ( isset( $_GET['settings-updated'] ) ) {
        add_settings_error(
            'prefix_messages',
            'prefix_message',
            __( 'Settings Saved', 'textdomain' ),
            'updated'
        );
    }

    // Show error/update messages.
    settings_errors( 'prefix_messages' );
    ?>
    <div class="wrap">
        <h1><?php echo esc_html( get_admin_page_title() ); ?></h1>
        <form action="options.php" method="post">
            <?php
            // Output security fields.
            settings_fields( 'prefix_settings_group' );
            // Output setting sections and fields.
            do_settings_sections( 'prefix-settings' );
            // Output save settings button.
            submit_button( __( 'Save Settings', 'textdomain' ) );
            ?>
        </form>
    </div>
    <?php
}

/**
 * Add settings link to plugin action links.
 *
 * @param array $links Plugin action links.
 * @return array Modified action links.
 */
function prefix_plugin_action_links( $links ) {
    $settings_link = sprintf(
        '<a href="%s">%s</a>',
        esc_url( admin_url( 'admin.php?page=prefix-settings' ) ),
        esc_html__( 'Settings', 'textdomain' )
    );
    array_unshift( $links, $settings_link );
    return $links;
}
add_filter( 'plugin_action_links_' . PREFIX_PLUGIN_BASENAME, 'prefix_plugin_action_links' );
```

---

## Options API & Transients

> **Reference**: https://developer.wordpress.org/apis/options/

### Options API

```php
<?php
/**
 * Options API usage examples.
 *
 * @package Prefix_Plugin
 */

// Get an option (with default value).
$value = get_option( 'prefix_option_name', 'default_value' );

// Update an option (creates if doesn't exist).
update_option( 'prefix_option_name', $new_value, $autoload = true );

// Add an option (only if it doesn't exist).
add_option( 'prefix_option_name', $value, '', $autoload = true );

// Delete an option.
delete_option( 'prefix_option_name' );

// Store complex data (arrays/objects are serialized automatically).
$settings = array(
    'enabled'       => true,
    'api_key'       => 'abc123',
    'items_per_page' => 10,
);
update_option( 'prefix_plugin_settings', $settings );

// Retrieve and use.
$settings = get_option( 'prefix_plugin_settings', array() );
$enabled = isset( $settings['enabled'] ) ? $settings['enabled'] : false;

// For network-wide options (Multisite).
get_site_option( 'prefix_network_option', 'default' );
update_site_option( 'prefix_network_option', $value );
delete_site_option( 'prefix_network_option' );
```

### Transients API

```php
<?php
/**
 * Transients API for temporary cached data.
 *
 * @package Prefix_Plugin
 */

/**
 * Get data with transient caching.
 *
 * @return array Cached or fresh data.
 */
function prefix_get_external_data() {
    $transient_key = 'prefix_external_data';
    
    // Try to get cached data.
    $data = get_transient( $transient_key );
    
    // If cache exists and is valid, return it.
    if ( false !== $data ) {
        return $data;
    }
    
    // Fetch fresh data (e.g., from external API).
    $response = wp_remote_get( 'https://api.example.com/data' );
    
    if ( is_wp_error( $response ) ) {
        return array();
    }
    
    $data = json_decode( wp_remote_retrieve_body( $response ), true );
    
    // Cache the data for 1 hour.
    set_transient( $transient_key, $data, HOUR_IN_SECONDS );
    
    return $data;
}

/**
 * Clear cached data when needed.
 *
 * @return void
 */
function prefix_clear_cache() {
    delete_transient( 'prefix_external_data' );
}

// Time constants available in WordPress:
// MINUTE_IN_SECONDS = 60
// HOUR_IN_SECONDS = 3600
// DAY_IN_SECONDS = 86400
// WEEK_IN_SECONDS = 604800
// MONTH_IN_SECONDS = 2592000 (30 days)
// YEAR_IN_SECONDS = 31536000

// Site transients (for Multisite network-wide caching).
set_site_transient( 'prefix_network_cache', $data, DAY_IN_SECONDS );
get_site_transient( 'prefix_network_cache' );
delete_site_transient( 'prefix_network_cache' );

/**
 * Example: Cache expensive database query.
 *
 * @return array Products data.
 */
function prefix_get_featured_products() {
    $cache_key = 'prefix_featured_products';
    $products  = get_transient( $cache_key );
    
    if ( false === $products ) {
        $products = get_posts( array(
            'post_type'      => 'product',
            'posts_per_page' => 10,
            'meta_key'       => '_featured',
            'meta_value'     => 'yes',
        ) );
        
        // Cache for 12 hours.
        set_transient( $cache_key, $products, 12 * HOUR_IN_SECONDS );
    }
    
    return $products;
}

/**
 * Invalidate cache when products are updated.
 *
 * @param int     $post_id Post ID.
 * @param WP_Post $post    Post object.
 * @return void
 */
function prefix_invalidate_product_cache( $post_id, $post ) {
    if ( 'product' === $post->post_type ) {
        delete_transient( 'prefix_featured_products' );
    }
}
add_action( 'save_post', 'prefix_invalidate_product_cache', 10, 2 );
```

---

## WordPress Cron & Scheduling

> **Reference**: https://developer.wordpress.org/plugins/cron/

### Scheduling Events

```php
<?php
/**
 * WordPress Cron implementation.
 *
 * @package Prefix_Plugin
 */

/**
 * Schedule cron events on plugin activation.
 *
 * @return void
 */
function prefix_activate_cron() {
    // Schedule single event.
    if ( ! wp_next_scheduled( 'prefix_daily_cleanup' ) ) {
        wp_schedule_event( time(), 'daily', 'prefix_daily_cleanup' );
    }
    
    // Schedule hourly event.
    if ( ! wp_next_scheduled( 'prefix_hourly_sync' ) ) {
        wp_schedule_event( time(), 'hourly', 'prefix_hourly_sync' );
    }
}
register_activation_hook( __FILE__, 'prefix_activate_cron' );

/**
 * Clear scheduled events on plugin deactivation.
 *
 * @return void
 */
function prefix_deactivate_cron() {
    wp_clear_scheduled_hook( 'prefix_daily_cleanup' );
    wp_clear_scheduled_hook( 'prefix_hourly_sync' );
}
register_deactivation_hook( __FILE__, 'prefix_deactivate_cron' );

/**
 * Add custom cron schedule intervals.
 *
 * @param array $schedules Existing schedules.
 * @return array Modified schedules.
 */
function prefix_add_cron_intervals( $schedules ) {
    // Add 5 minutes interval.
    $schedules['five_minutes'] = array(
        'interval' => 5 * MINUTE_IN_SECONDS,
        'display'  => __( 'Every Five Minutes', 'textdomain' ),
    );
    
    // Add 15 minutes interval.
    $schedules['fifteen_minutes'] = array(
        'interval' => 15 * MINUTE_IN_SECONDS,
        'display'  => __( 'Every Fifteen Minutes', 'textdomain' ),
    );
    
    // Add twice daily (12 hours).
    $schedules['twicedaily'] = array(
        'interval' => 12 * HOUR_IN_SECONDS,
        'display'  => __( 'Twice Daily', 'textdomain' ),
    );
    
    // Add weekly.
    $schedules['weekly'] = array(
        'interval' => WEEK_IN_SECONDS,
        'display'  => __( 'Once Weekly', 'textdomain' ),
    );
    
    return $schedules;
}
add_filter( 'cron_schedules', 'prefix_add_cron_intervals' );

/**
 * Daily cleanup task.
 *
 * @return void
 */
function prefix_do_daily_cleanup() {
    global $wpdb;
    
    // Example: Delete old log entries.
    $wpdb->query(
        $wpdb->prepare(
            "DELETE FROM {$wpdb->prefix}prefix_logs WHERE created_at < %s",
            gmdate( 'Y-m-d H:i:s', strtotime( '-30 days' ) )
        )
    );
    
    // Clear old transients.
    delete_expired_transients( true );
    
    // Log completion.
    error_log( 'Prefix Plugin: Daily cleanup completed at ' . current_time( 'mysql' ) );
}
add_action( 'prefix_daily_cleanup', 'prefix_do_daily_cleanup' );

/**
 * Hourly sync task.
 *
 * @return void
 */
function prefix_do_hourly_sync() {
    // Perform sync operation.
    $result = prefix_sync_external_data();
    
    if ( is_wp_error( $result ) ) {
        error_log( 'Prefix Plugin: Sync failed - ' . $result->get_error_message() );
    }
}
add_action( 'prefix_hourly_sync', 'prefix_do_hourly_sync' );

/**
 * Schedule a single one-time event.
 *
 * @param int $user_id User ID.
 * @return void
 */
function prefix_schedule_welcome_email( $user_id ) {
    // Schedule email to be sent in 1 hour.
    wp_schedule_single_event(
        time() + HOUR_IN_SECONDS,
        'prefix_send_welcome_email',
        array( $user_id )
    );
}

/**
 * Send welcome email (cron callback with arguments).
 *
 * @param int $user_id User ID.
 * @return void
 */
function prefix_send_welcome_email_callback( $user_id ) {
    $user = get_userdata( $user_id );
    if ( ! $user ) {
        return;
    }
    
    wp_mail(
        $user->user_email,
        __( 'Welcome!', 'textdomain' ),
        __( 'Thank you for registering.', 'textdomain' )
    );
}
add_action( 'prefix_send_welcome_email', 'prefix_send_welcome_email_callback' );

// Check if event is scheduled.
$next_scheduled = wp_next_scheduled( 'prefix_daily_cleanup' );
if ( $next_scheduled ) {
    echo 'Next run: ' . gmdate( 'Y-m-d H:i:s', $next_scheduled );
}

// Unschedule specific event with arguments.
$timestamp = wp_next_scheduled( 'prefix_send_welcome_email', array( $user_id ) );
if ( $timestamp ) {
    wp_unschedule_event( $timestamp, 'prefix_send_welcome_email', array( $user_id ) );
}
```

---

## User Roles & Capabilities

> **Reference**: https://developer.wordpress.org/plugins/users/roles-and-capabilities/

### Working with Roles and Capabilities

```php
<?php
/**
 * User roles and capabilities.
 *
 * @package Prefix_Plugin
 */

/**
 * Add custom role on plugin activation.
 *
 * @return void
 */
function prefix_add_custom_roles() {
    // Add custom role.
    add_role(
        'prefix_manager',                          // Role slug.
        __( 'Plugin Manager', 'textdomain' ),     // Display name.
        array(
            'read'                  => true,
            'edit_posts'            => true,
            'delete_posts'          => false,
            'upload_files'          => true,
            'prefix_manage_settings' => true,      // Custom capability.
            'prefix_view_reports'   => true,       // Custom capability.
        )
    );

    // Add capabilities to existing roles.
    $admin = get_role( 'administrator' );
    if ( $admin ) {
        $admin->add_cap( 'prefix_manage_settings' );
        $admin->add_cap( 'prefix_view_reports' );
        $admin->add_cap( 'prefix_manage_all' );
    }

    $editor = get_role( 'editor' );
    if ( $editor ) {
        $editor->add_cap( 'prefix_view_reports' );
    }
}
register_activation_hook( __FILE__, 'prefix_add_custom_roles' );

/**
 * Remove custom role and capabilities on plugin deactivation.
 *
 * @return void
 */
function prefix_remove_custom_roles() {
    // Remove custom role.
    remove_role( 'prefix_manager' );

    // Remove capabilities from existing roles.
    $roles = array( 'administrator', 'editor' );
    foreach ( $roles as $role_name ) {
        $role = get_role( $role_name );
        if ( $role ) {
            $role->remove_cap( 'prefix_manage_settings' );
            $role->remove_cap( 'prefix_view_reports' );
            $role->remove_cap( 'prefix_manage_all' );
        }
    }
}
register_deactivation_hook( __FILE__, 'prefix_remove_custom_roles' );

/**
 * Check capabilities before performing actions.
 *
 * @return void
 */
function prefix_admin_settings_page() {
    // Check user capability.
    if ( ! current_user_can( 'prefix_manage_settings' ) ) {
        wp_die(
            esc_html__( 'You do not have permission to access this page.', 'textdomain' ),
            esc_html__( 'Permission Denied', 'textdomain' ),
            array( 'response' => 403 )
        );
    }

    // Render settings page.
}

/**
 * Custom capability mapping for custom post type.
 *
 * @return void
 */
function prefix_register_cpt_with_capabilities() {
    register_post_type( 'prefix_resource', array(
        'labels'       => array( /* ... */ ),
        'public'       => true,
        'capability_type' => array( 'prefix_resource', 'prefix_resources' ),
        'map_meta_cap' => true,
        'capabilities' => array(
            // Meta capabilities (mapped by WordPress).
            'edit_post'          => 'edit_prefix_resource',
            'read_post'          => 'read_prefix_resource',
            'delete_post'        => 'delete_prefix_resource',
            // Primitive capabilities.
            'edit_posts'         => 'edit_prefix_resources',
            'edit_others_posts'  => 'edit_others_prefix_resources',
            'publish_posts'      => 'publish_prefix_resources',
            'read_private_posts' => 'read_private_prefix_resources',
            'delete_posts'       => 'delete_prefix_resources',
            'delete_private_posts' => 'delete_private_prefix_resources',
            'delete_published_posts' => 'delete_published_prefix_resources',
            'delete_others_posts' => 'delete_others_prefix_resources',
            'edit_private_posts' => 'edit_private_prefix_resources',
            'edit_published_posts' => 'edit_published_prefix_resources',
            'create_posts'       => 'create_prefix_resources',
        ),
        'show_in_rest' => true,
    ) );
}
add_action( 'init', 'prefix_register_cpt_with_capabilities' );

/**
 * Grant custom post type capabilities to roles.
 *
 * @return void
 */
function prefix_grant_cpt_capabilities() {
    $admin = get_role( 'administrator' );
    if ( ! $admin ) {
        return;
    }

    $capabilities = array(
        'edit_prefix_resource',
        'read_prefix_resource',
        'delete_prefix_resource',
        'edit_prefix_resources',
        'edit_others_prefix_resources',
        'publish_prefix_resources',
        'read_private_prefix_resources',
        'delete_prefix_resources',
        'delete_private_prefix_resources',
        'delete_published_prefix_resources',
        'delete_others_prefix_resources',
        'edit_private_prefix_resources',
        'edit_published_prefix_resources',
        'create_prefix_resources',
    );

    foreach ( $capabilities as $cap ) {
        $admin->add_cap( $cap );
    }
}

// Check specific user capability.
if ( user_can( $user_id, 'prefix_manage_settings' ) ) {
    // User has capability.
}

// Check current user capability.
if ( current_user_can( 'edit_posts' ) ) {
    // Current user can edit posts.
}

// Check capability for specific post.
if ( current_user_can( 'edit_post', $post_id ) ) {
    // Current user can edit this specific post.
}
```

---

## Shortcodes Development

> **Reference**: https://developer.wordpress.org/plugins/shortcodes/

### Creating Shortcodes

```php
<?php
/**
 * Shortcode implementation.
 *
 * @package Prefix_Plugin
 */

/**
 * Simple shortcode.
 * Usage: [prefix_greeting]
 *
 * @return string Shortcode output.
 */
function prefix_greeting_shortcode() {
    return '<p class="prefix-greeting">' . esc_html__( 'Hello, World!', 'textdomain' ) . '</p>';
}
add_shortcode( 'prefix_greeting', 'prefix_greeting_shortcode' );

/**
 * Shortcode with attributes.
 * Usage: [prefix_button text="Click Me" url="https://example.com" color="blue" size="large"]
 *
 * @param array  $atts    Shortcode attributes.
 * @param string $content Enclosed content.
 * @return string Shortcode output.
 */
function prefix_button_shortcode( $atts, $content = null ) {
    // Define default attributes and parse user attributes.
    $atts = shortcode_atts(
        array(
            'text'   => __( 'Click Here', 'textdomain' ),
            'url'    => '#',
            'color'  => 'primary',
            'size'   => 'medium',
            'target' => '_self',
            'class'  => '',
        ),
        $atts,
        'prefix_button' // Shortcode name for filtering.
    );

    // Sanitize attributes.
    $text   = sanitize_text_field( $atts['text'] );
    $url    = esc_url( $atts['url'] );
    $color  = sanitize_html_class( $atts['color'] );
    $size   = sanitize_html_class( $atts['size'] );
    $target = in_array( $atts['target'], array( '_self', '_blank' ), true ) ? $atts['target'] : '_self';
    $class  = sanitize_html_class( $atts['class'] );

    // Build CSS classes.
    $classes = array(
        'prefix-button',
        'prefix-button--' . $color,
        'prefix-button--' . $size,
    );
    
    if ( ! empty( $class ) ) {
        $classes[] = $class;
    }

    // Build output.
    $output = sprintf(
        '<a href="%s" class="%s" target="%s"%s>%s</a>',
        $url,
        esc_attr( implode( ' ', $classes ) ),
        esc_attr( $target ),
        '_blank' === $target ? ' rel="noopener noreferrer"' : '',
        esc_html( $text )
    );

    return $output;
}
add_shortcode( 'prefix_button', 'prefix_button_shortcode' );

/**
 * Enclosing shortcode (with content).
 * Usage: [prefix_box title="My Box" type="info"]Content here[/prefix_box]
 *
 * @param array  $atts    Shortcode attributes.
 * @param string $content Enclosed content.
 * @return string Shortcode output.
 */
function prefix_box_shortcode( $atts, $content = null ) {
    $atts = shortcode_atts(
        array(
            'title' => '',
            'type'  => 'default',
            'icon'  => '',
        ),
        $atts,
        'prefix_box'
    );

    $type  = sanitize_html_class( $atts['type'] );
    $title = sanitize_text_field( $atts['title'] );
    $icon  = sanitize_html_class( $atts['icon'] );

    ob_start();
    ?>
    <div class="prefix-box prefix-box--<?php echo esc_attr( $type ); ?>">
        <?php if ( ! empty( $title ) ) : ?>
            <div class="prefix-box__header">
                <?php if ( ! empty( $icon ) ) : ?>
                    <span class="prefix-box__icon dashicons dashicons-<?php echo esc_attr( $icon ); ?>"></span>
                <?php endif; ?>
                <h4 class="prefix-box__title"><?php echo esc_html( $title ); ?></h4>
            </div>
        <?php endif; ?>
        <div class="prefix-box__content">
            <?php
            // Process nested shortcodes and apply content filters.
            echo wp_kses_post( do_shortcode( $content ) );
            ?>
        </div>
    </div>
    <?php
    return ob_get_clean();
}
add_shortcode( 'prefix_box', 'prefix_box_shortcode' );

/**
 * Shortcode with WP_Query.
 * Usage: [prefix_posts count="5" category="news" orderby="date"]
 *
 * @param array $atts Shortcode attributes.
 * @return string Shortcode output.
 */
function prefix_posts_shortcode( $atts ) {
    $atts = shortcode_atts(
        array(
            'count'     => 5,
            'category'  => '',
            'orderby'   => 'date',
            'order'     => 'DESC',
            'post_type' => 'post',
        ),
        $atts,
        'prefix_posts'
    );

    $args = array(
        'post_type'      => sanitize_key( $atts['post_type'] ),
        'posts_per_page' => absint( $atts['count'] ),
        'orderby'        => sanitize_key( $atts['orderby'] ),
        'order'          => in_array( strtoupper( $atts['order'] ), array( 'ASC', 'DESC' ), true ) 
            ? strtoupper( $atts['order'] ) 
            : 'DESC',
        'post_status'    => 'publish',
    );

    if ( ! empty( $atts['category'] ) ) {
        $args['category_name'] = sanitize_title( $atts['category'] );
    }

    $query = new WP_Query( $args );

    if ( ! $query->have_posts() ) {
        return '<p>' . esc_html__( 'No posts found.', 'textdomain' ) . '</p>';
    }

    ob_start();
    ?>
    <ul class="prefix-posts-list">
        <?php
        while ( $query->have_posts() ) {
            $query->the_post();
            ?>
            <li class="prefix-posts-list__item">
                <a href="<?php the_permalink(); ?>">
                    <?php the_title(); ?>
                </a>
                <span class="prefix-posts-list__date">
                    <?php echo esc_html( get_the_date() ); ?>
                </span>
            </li>
            <?php
        }
        wp_reset_postdata();
        ?>
    </ul>
    <?php
    return ob_get_clean();
}
add_shortcode( 'prefix_posts', 'prefix_posts_shortcode' );

/**
 * Register shortcode for use in Gutenberg.
 *
 * @return void
 */
function prefix_register_shortcode_block() {
    // Shortcodes work in Gutenberg via the Shortcode block.
    // For better integration, consider creating a proper Gutenberg block.
}
```

---

## Classic Widget Development

> **Reference**: https://developer.wordpress.org/plugins/widgets/

### Creating a Widget

```php
<?php
/**
 * Custom widget class.
 *
 * @package Prefix_Plugin
 */

/**
 * Class Prefix_Recent_Posts_Widget
 *
 * Displays recent posts with thumbnails.
 */
class Prefix_Recent_Posts_Widget extends WP_Widget {

    /**
     * Constructor.
     */
    public function __construct() {
        parent::__construct(
            'prefix_recent_posts',                 // Widget ID.
            __( 'Prefix Recent Posts', 'textdomain' ), // Widget name.
            array(
                'classname'                   => 'prefix-recent-posts-widget',
                'description'                 => __( 'Displays recent posts with thumbnails.', 'textdomain' ),
                'customize_selective_refresh' => true,
            )
        );
    }

    /**
     * Front-end display of widget.
     *
     * @param array $args     Widget arguments.
     * @param array $instance Widget instance settings.
     * @return void
     */
    public function widget( $args, $instance ) {
        $title         = ! empty( $instance['title'] ) ? $instance['title'] : __( 'Recent Posts', 'textdomain' );
        $title         = apply_filters( 'widget_title', $title, $instance, $this->id_base );
        $number        = ! empty( $instance['number'] ) ? absint( $instance['number'] ) : 5;
        $show_date     = isset( $instance['show_date'] ) ? $instance['show_date'] : false;
        $show_thumbnail = isset( $instance['show_thumbnail'] ) ? $instance['show_thumbnail'] : true;

        $query_args = array(
            'posts_per_page'      => $number,
            'no_found_rows'       => true,
            'post_status'         => 'publish',
            'ignore_sticky_posts' => true,
        );

        $recent_posts = new WP_Query( $query_args );

        if ( ! $recent_posts->have_posts() ) {
            return;
        }

        echo $args['before_widget']; // phpcs:ignore WordPress.Security.EscapeOutput.OutputNotEscaped

        if ( $title ) {
            echo $args['before_title'] . esc_html( $title ) . $args['after_title']; // phpcs:ignore WordPress.Security.EscapeOutput.OutputNotEscaped
        }
        ?>
        <ul class="prefix-recent-posts">
            <?php
            while ( $recent_posts->have_posts() ) {
                $recent_posts->the_post();
                ?>
                <li class="prefix-recent-posts__item">
                    <?php if ( $show_thumbnail && has_post_thumbnail() ) : ?>
                        <div class="prefix-recent-posts__thumbnail">
                            <a href="<?php the_permalink(); ?>">
                                <?php the_post_thumbnail( 'thumbnail' ); ?>
                            </a>
                        </div>
                    <?php endif; ?>
                    <div class="prefix-recent-posts__content">
                        <a href="<?php the_permalink(); ?>" class="prefix-recent-posts__title">
                            <?php the_title(); ?>
                        </a>
                        <?php if ( $show_date ) : ?>
                            <span class="prefix-recent-posts__date">
                                <?php echo esc_html( get_the_date() ); ?>
                            </span>
                        <?php endif; ?>
                    </div>
                </li>
                <?php
            }
            wp_reset_postdata();
            ?>
        </ul>
        <?php
        echo $args['after_widget']; // phpcs:ignore WordPress.Security.EscapeOutput.OutputNotEscaped
    }

    /**
     * Back-end widget form.
     *
     * @param array $instance Previously saved values from database.
     * @return void
     */
    public function form( $instance ) {
        $title          = isset( $instance['title'] ) ? $instance['title'] : __( 'Recent Posts', 'textdomain' );
        $number         = isset( $instance['number'] ) ? absint( $instance['number'] ) : 5;
        $show_date      = isset( $instance['show_date'] ) ? (bool) $instance['show_date'] : false;
        $show_thumbnail = isset( $instance['show_thumbnail'] ) ? (bool) $instance['show_thumbnail'] : true;
        ?>
        <p>
            <label for="<?php echo esc_attr( $this->get_field_id( 'title' ) ); ?>">
                <?php esc_html_e( 'Title:', 'textdomain' ); ?>
            </label>
            <input 
                class="widefat" 
                id="<?php echo esc_attr( $this->get_field_id( 'title' ) ); ?>" 
                name="<?php echo esc_attr( $this->get_field_name( 'title' ) ); ?>" 
                type="text" 
                value="<?php echo esc_attr( $title ); ?>"
            />
        </p>
        <p>
            <label for="<?php echo esc_attr( $this->get_field_id( 'number' ) ); ?>">
                <?php esc_html_e( 'Number of posts to show:', 'textdomain' ); ?>
            </label>
            <input 
                class="tiny-text" 
                id="<?php echo esc_attr( $this->get_field_id( 'number' ) ); ?>" 
                name="<?php echo esc_attr( $this->get_field_name( 'number' ) ); ?>" 
                type="number" 
                step="1" 
                min="1" 
                max="20" 
                value="<?php echo esc_attr( $number ); ?>" 
                size="3"
            />
        </p>
        <p>
            <input 
                class="checkbox" 
                type="checkbox" 
                <?php checked( $show_date ); ?> 
                id="<?php echo esc_attr( $this->get_field_id( 'show_date' ) ); ?>" 
                name="<?php echo esc_attr( $this->get_field_name( 'show_date' ) ); ?>"
            />
            <label for="<?php echo esc_attr( $this->get_field_id( 'show_date' ) ); ?>">
                <?php esc_html_e( 'Display post date?', 'textdomain' ); ?>
            </label>
        </p>
        <p>
            <input 
                class="checkbox" 
                type="checkbox" 
                <?php checked( $show_thumbnail ); ?> 
                id="<?php echo esc_attr( $this->get_field_id( 'show_thumbnail' ) ); ?>" 
                name="<?php echo esc_attr( $this->get_field_name( 'show_thumbnail' ) ); ?>"
            />
            <label for="<?php echo esc_attr( $this->get_field_id( 'show_thumbnail' ) ); ?>">
                <?php esc_html_e( 'Display post thumbnail?', 'textdomain' ); ?>
            </label>
        </p>
        <?php
    }

    /**
     * Sanitize widget form values as they are saved.
     *
     * @param array $new_instance Values just sent to be saved.
     * @param array $old_instance Previously saved values from database.
     * @return array Updated safe values to be saved.
     */
    public function update( $new_instance, $old_instance ) {
        $instance = $old_instance;
        
        $instance['title']          = sanitize_text_field( $new_instance['title'] );
        $instance['number']         = absint( $new_instance['number'] );
        $instance['show_date']      = isset( $new_instance['show_date'] ) ? (bool) $new_instance['show_date'] : false;
        $instance['show_thumbnail'] = isset( $new_instance['show_thumbnail'] ) ? (bool) $new_instance['show_thumbnail'] : false;

        return $instance;
    }
}

/**
 * Register widget.
 *
 * @return void
 */
function prefix_register_widgets() {
    register_widget( 'Prefix_Recent_Posts_Widget' );
}
add_action( 'widgets_init', 'prefix_register_widgets' );
```

---

## theme.json Block Theme Configuration

> **Reference**: https://developer.wordpress.org/block-editor/how-to-guides/themes/global-settings-and-styles/

### Complete theme.json Structure

```json
{
    "$schema": "https://schemas.wp.org/trunk/theme.json",
    "version": 3,
    "settings": {
        "appearanceTools": true,
        "useRootPaddingAwareAlignments": true,
        "layout": {
            "contentSize": "840px",
            "wideSize": "1200px"
        },
        "spacing": {
            "padding": true,
            "margin": true,
            "blockGap": true,
            "units": ["px", "em", "rem", "%", "vh", "vw"],
            "spacingSizes": [
                {
                    "name": "XS",
                    "size": "0.5rem",
                    "slug": "xs"
                },
                {
                    "name": "Small",
                    "size": "1rem",
                    "slug": "small"
                },
                {
                    "name": "Medium",
                    "size": "1.5rem",
                    "slug": "medium"
                },
                {
                    "name": "Large",
                    "size": "2rem",
                    "slug": "large"
                },
                {
                    "name": "XL",
                    "size": "3rem",
                    "slug": "xl"
                }
            ]
        },
        "color": {
            "custom": true,
            "customGradient": true,
            "customDuotone": true,
            "defaultPalette": false,
            "defaultGradients": false,
            "defaultDuotone": false,
            "palette": [
                {
                    "name": "Primary",
                    "slug": "primary",
                    "color": "#0066cc"
                },
                {
                    "name": "Secondary",
                    "slug": "secondary",
                    "color": "#6c757d"
                },
                {
                    "name": "Accent",
                    "slug": "accent",
                    "color": "#ff6b35"
                },
                {
                    "name": "Background",
                    "slug": "background",
                    "color": "#ffffff"
                },
                {
                    "name": "Foreground",
                    "slug": "foreground",
                    "color": "#1a1a1a"
                },
                {
                    "name": "Light Gray",
                    "slug": "light-gray",
                    "color": "#f8f9fa"
                }
            ],
            "gradients": [
                {
                    "name": "Primary to Secondary",
                    "slug": "primary-to-secondary",
                    "gradient": "linear-gradient(135deg, var(--wp--preset--color--primary) 0%, var(--wp--preset--color--secondary) 100%)"
                }
            ]
        },
        "typography": {
            "customFontSize": true,
            "dropCap": true,
            "fluid": true,
            "fontFamilies": [
                {
                    "fontFamily": "-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif",
                    "name": "System Font",
                    "slug": "system-font"
                },
                {
                    "fontFamily": "'Inter', sans-serif",
                    "name": "Inter",
                    "slug": "inter",
                    "fontFace": [
                        {
                            "fontFamily": "Inter",
                            "fontWeight": "400",
                            "fontStyle": "normal",
                            "src": ["file:./assets/fonts/inter/Inter-Regular.woff2"]
                        },
                        {
                            "fontFamily": "Inter",
                            "fontWeight": "700",
                            "fontStyle": "normal",
                            "src": ["file:./assets/fonts/inter/Inter-Bold.woff2"]
                        }
                    ]
                }
            ],
            "fontSizes": [
                {
                    "name": "Small",
                    "slug": "small",
                    "size": "0.875rem",
                    "fluid": {
                        "min": "0.875rem",
                        "max": "1rem"
                    }
                },
                {
                    "name": "Medium",
                    "slug": "medium",
                    "size": "1rem",
                    "fluid": {
                        "min": "1rem",
                        "max": "1.125rem"
                    }
                },
                {
                    "name": "Large",
                    "slug": "large",
                    "size": "1.25rem",
                    "fluid": {
                        "min": "1.125rem",
                        "max": "1.5rem"
                    }
                },
                {
                    "name": "X-Large",
                    "slug": "x-large",
                    "size": "2rem",
                    "fluid": {
                        "min": "1.5rem",
                        "max": "2.5rem"
                    }
                },
                {
                    "name": "XX-Large",
                    "slug": "xx-large",
                    "size": "3rem",
                    "fluid": {
                        "min": "2rem",
                        "max": "4rem"
                    }
                }
            ]
        },
        "border": {
            "color": true,
            "radius": true,
            "style": true,
            "width": true
        },
        "shadow": {
            "presets": [
                {
                    "name": "Small",
                    "slug": "small",
                    "shadow": "0 1px 3px rgba(0,0,0,0.12)"
                },
                {
                    "name": "Medium",
                    "slug": "medium",
                    "shadow": "0 4px 6px rgba(0,0,0,0.1)"
                },
                {
                    "name": "Large",
                    "slug": "large",
                    "shadow": "0 10px 15px rgba(0,0,0,0.1)"
                }
            ]
        },
        "blocks": {
            "core/button": {
                "border": {
                    "radius": true
                }
            },
            "core/paragraph": {
                "typography": {
                    "dropCap": true
                }
            }
        }
    },
    "styles": {
        "color": {
            "background": "var(--wp--preset--color--background)",
            "text": "var(--wp--preset--color--foreground)"
        },
        "typography": {
            "fontFamily": "var(--wp--preset--font-family--system-font)",
            "fontSize": "var(--wp--preset--font-size--medium)",
            "lineHeight": "1.6"
        },
        "spacing": {
            "padding": {
                "top": "0",
                "right": "var(--wp--preset--spacing--medium)",
                "bottom": "0",
                "left": "var(--wp--preset--spacing--medium)"
            }
        },
        "elements": {
            "link": {
                "color": {
                    "text": "var(--wp--preset--color--primary)"
                },
                ":hover": {
                    "color": {
                        "text": "var(--wp--preset--color--secondary)"
                    }
                }
            },
            "h1": {
                "typography": {
                    "fontSize": "var(--wp--preset--font-size--xx-large)",
                    "fontWeight": "700",
                    "lineHeight": "1.2"
                }
            },
            "h2": {
                "typography": {
                    "fontSize": "var(--wp--preset--font-size--x-large)",
                    "fontWeight": "700",
                    "lineHeight": "1.3"
                }
            },
            "button": {
                "color": {
                    "background": "var(--wp--preset--color--primary)",
                    "text": "#ffffff"
                },
                "border": {
                    "radius": "4px"
                },
                ":hover": {
                    "color": {
                        "background": "var(--wp--preset--color--secondary)"
                    }
                }
            }
        },
        "blocks": {
            "core/site-title": {
                "typography": {
                    "fontSize": "var(--wp--preset--font-size--large)",
                    "fontWeight": "700"
                }
            },
            "core/navigation": {
                "typography": {
                    "fontSize": "var(--wp--preset--font-size--small)"
                }
            }
        }
    },
    "templateParts": [
        {
            "name": "header",
            "title": "Header",
            "area": "header"
        },
        {
            "name": "footer",
            "title": "Footer",
            "area": "footer"
        },
        {
            "name": "sidebar",
            "title": "Sidebar",
            "area": "uncategorized"
        }
    ],
    "customTemplates": [
        {
            "name": "page-full-width",
            "title": "Full Width",
            "postTypes": ["page"]
        },
        {
            "name": "page-sidebar",
            "title": "Page with Sidebar",
            "postTypes": ["page", "post"]
        }
    ],
    "patterns": [
        "featured-posts",
        "hero-section"
    ]
}
```

---

## WP-CLI Development

> **Reference**: https://make.wordpress.org/cli/handbook/

### Creating Custom WP-CLI Commands

```php
<?php
/**
 * WP-CLI custom commands.
 *
 * @package Prefix_Plugin
 */

// Only load in WP-CLI context.
if ( ! defined( 'WP_CLI' ) || ! WP_CLI ) {
    return;
}

/**
 * Custom WP-CLI commands for Prefix Plugin.
 */
class Prefix_CLI_Commands {

    /**
     * Clears plugin cache.
     *
     * ## OPTIONS
     *
     * [--all]
     * : Clear all cache types.
     *
     * [--type=<type>]
     * : Specific cache type to clear.
     * ---
     * default: all
     * options:
     *   - all
     *   - transients
     *   - data
     * ---
     *
     * ## EXAMPLES
     *
     *     # Clear all cache
     *     $ wp prefix cache clear --all
     *
     *     # Clear only transients
     *     $ wp prefix cache clear --type=transients
     *
     * @param array $args       Positional arguments.
     * @param array $assoc_args Associative arguments.
     * @return void
     */
    public function clear( $args, $assoc_args ) {
        $type = WP_CLI\Utils\get_flag_value( $assoc_args, 'type', 'all' );

        if ( 'all' === $type || 'transients' === $type ) {
            global $wpdb;
            $wpdb->query( "DELETE FROM {$wpdb->options} WHERE option_name LIKE '_transient_prefix_%'" );
            $wpdb->query( "DELETE FROM {$wpdb->options} WHERE option_name LIKE '_transient_timeout_prefix_%'" );
            WP_CLI::success( 'Transients cleared.' );
        }

        if ( 'all' === $type || 'data' === $type ) {
            delete_option( 'prefix_cached_data' );
            WP_CLI::success( 'Data cache cleared.' );
        }

        WP_CLI::success( 'Cache clearing complete.' );
    }

    /**
     * Exports plugin data.
     *
     * ## OPTIONS
     *
     * <file>
     * : Output file path.
     *
     * [--format=<format>]
     * : Output format.
     * ---
     * default: json
     * options:
     *   - json
     *   - csv
     * ---
     *
     * ## EXAMPLES
     *
     *     $ wp prefix export /tmp/data.json
     *     $ wp prefix export /tmp/data.csv --format=csv
     *
     * @param array $args       Positional arguments.
     * @param array $assoc_args Associative arguments.
     * @return void
     */
    public function export( $args, $assoc_args ) {
        list( $file ) = $args;
        $format = WP_CLI\Utils\get_flag_value( $assoc_args, 'format', 'json' );

        // Get data to export.
        $data = prefix_get_export_data();

        if ( empty( $data ) ) {
            WP_CLI::error( 'No data to export.' );
        }

        if ( 'json' === $format ) {
            $content = wp_json_encode( $data, JSON_PRETTY_PRINT );
        } else {
            // CSV format.
            $content = prefix_array_to_csv( $data );
        }

        // Write to file.
        $result = file_put_contents( $file, $content ); // phpcs:ignore WordPress.WP.AlternativeFunctions.file_system_read_file_put_contents

        if ( false === $result ) {
            WP_CLI::error( 'Failed to write file.' );
        }

        WP_CLI::success( sprintf( 'Data exported to %s', $file ) );
    }

    /**
     * Runs database migrations.
     *
     * ## EXAMPLES
     *
     *     $ wp prefix migrate
     *
     * @param array $args       Positional arguments.
     * @param array $assoc_args Associative arguments.
     * @return void
     */
    public function migrate( $args, $assoc_args ) {
        WP_CLI::log( 'Starting database migration...' );

        $progress = \WP_CLI\Utils\make_progress_bar( 'Migrating', 100 );

        for ( $i = 0; $i < 100; $i++ ) {
            // Simulate migration work.
            usleep( 10000 );
            $progress->tick();
        }

        $progress->finish();

        WP_CLI::success( 'Migration complete.' );
    }

    /**
     * Lists all items.
     *
     * ## OPTIONS
     *
     * [--format=<format>]
     * : Output format.
     * ---
     * default: table
     * options:
     *   - table
     *   - json
     *   - csv
     *   - yaml
     * ---
     *
     * ## EXAMPLES
     *
     *     $ wp prefix list
     *     $ wp prefix list --format=json
     *
     * @param array $args       Positional arguments.
     * @param array $assoc_args Associative arguments.
     * @return void
     */
    public function list_items( $args, $assoc_args ) {
        $items = array(
            array(
                'id'     => 1,
                'name'   => 'Item One',
                'status' => 'active',
            ),
            array(
                'id'     => 2,
                'name'   => 'Item Two',
                'status' => 'inactive',
            ),
        );

        $format = WP_CLI\Utils\get_flag_value( $assoc_args, 'format', 'table' );

        WP_CLI\Utils\format_items( $format, $items, array( 'id', 'name', 'status' ) );
    }
}

// Register commands.
WP_CLI::add_command( 'prefix cache', array( 'Prefix_CLI_Commands', 'clear' ) );
WP_CLI::add_command( 'prefix export', array( 'Prefix_CLI_Commands', 'export' ) );
WP_CLI::add_command( 'prefix migrate', array( 'Prefix_CLI_Commands', 'migrate' ) );
WP_CLI::add_command( 'prefix list', array( 'Prefix_CLI_Commands', 'list_items' ) );
```

### Useful WP-CLI Commands Reference

```bash
# Plugin management
wp plugin install plugin-name --activate
wp plugin deactivate plugin-name
wp plugin update --all

# Theme management
wp theme activate theme-name
wp theme update --all

# Database operations
wp db export backup.sql
wp db import backup.sql
wp db query "SELECT * FROM wp_options LIMIT 10"

# Options
wp option get blogname
wp option update blogname "New Site Name"
wp option delete prefix_plugin_settings

# Transients
wp transient get prefix_cache_key
wp transient delete prefix_cache_key
wp transient delete --all

# Posts
wp post list --post_type=post --posts_per_page=10
wp post create --post_title="New Post" --post_status=publish
wp post delete 123 --force

# Users
wp user create newuser newuser@example.com --role=subscriber
wp user update 1 --display_name="Admin User"

# Search and replace
wp search-replace 'old-domain.com' 'new-domain.com' --dry-run
wp search-replace 'old-domain.com' 'new-domain.com' --all-tables

# Cache
wp cache flush

# Rewrite rules
wp rewrite flush
wp rewrite structure '/%postname%/'

# Cron
wp cron event list
wp cron event run prefix_daily_cleanup
wp cron schedule list

# Maintenance mode
wp maintenance-mode activate
wp maintenance-mode deactivate

# Generate test data
wp post generate --count=50
wp user generate --count=10
wp term generate category --count=20
```

---

## Documentation References

### Official WordPress Documentation
- [WordPress Developer Resources](https://developer.wordpress.org/)
- [WordPress Coding Standards](https://developer.wordpress.org/coding-standards/wordpress-coding-standards/)
- [Plugin Handbook](https://developer.wordpress.org/plugins/)
- [Theme Handbook](https://developer.wordpress.org/themes/)
- [Block Editor Handbook](https://developer.wordpress.org/block-editor/)
- [REST API Handbook](https://developer.wordpress.org/rest-api/)
- [Common APIs Handbook](https://developer.wordpress.org/apis/)
- [Advanced Administration Handbook](https://developer.wordpress.org/advanced-administration/)
- [Custom Post Types](https://developer.wordpress.org/plugins/post-types/)
- [Custom Taxonomies](https://developer.wordpress.org/plugins/taxonomies/)
- [Settings API](https://developer.wordpress.org/plugins/settings/)
- [Options API](https://developer.wordpress.org/apis/options/)
- [Transients API](https://developer.wordpress.org/apis/transients/)
- [Cron / Scheduling](https://developer.wordpress.org/plugins/cron/)
- [User Roles & Capabilities](https://developer.wordpress.org/plugins/users/roles-and-capabilities/)
- [Shortcodes API](https://developer.wordpress.org/plugins/shortcodes/)
- [Widgets API](https://developer.wordpress.org/plugins/widgets/)
- [theme.json Reference](https://developer.wordpress.org/block-editor/how-to-guides/themes/global-settings-and-styles/)
- [Full Site Editing](https://fullsiteediting.com/)
- [WP-CLI Handbook](https://make.wordpress.org/cli/handbook/)

### WooCommerce Documentation
- [WooCommerce Developer Docs](https://developer.woocommerce.com/docs/)
- [WooCommerce Hooks Reference](https://woocommerce.github.io/code-reference/hooks/hooks.html)
- [WooCommerce Extension Development](https://developer.woocommerce.com/docs/woocommerce-extension-development-best-practices/)

### Elementor Documentation
- [Elementor Developers](https://developers.elementor.com/docs/)
- [Elementor Widget Development](https://developers.elementor.com/docs/widgets/)

### Crocoblock/JetEngine/JetFormBuilder
- [JetEngine Knowledge Base](https://crocoblock.com/knowledge-base/plugins/jetengine/)
- [JetFormBuilder Documentation](https://jetformbuilder.com/)
- [Crocoblock Developer Tools](https://github.com/Crocoblock)

---

*This document represents the definitive coding standards for world-class WordPress and WooCommerce development. All code should be reviewed against these standards before deployment.*

**Version**: 2.1.0  
**Last Updated**: December 2025  
**Maintained by**: NexaLance Development Team

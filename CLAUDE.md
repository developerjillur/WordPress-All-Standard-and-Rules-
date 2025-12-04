# Project Instructions for Claude Code

> **This file is automatically read by Claude Code at the start of every session.**
> All instructions here will be followed without needing to mention them in prompts.

---

## Project Type: WordPress Plugin/Theme Development

This project follows strict coding standards for:
- WordPress.org Plugin Directory submission
- CodeCanyon/Envato Marketplace submission
- Professional WordPress development best practices

---

## Required Reading Before Any Code Generation

Before writing ANY WordPress plugin or theme code, Claude MUST read and follow the guidelines in these files:

### 1. Claude Rules (General AI Behavior)
**Location:** `.claude/docs/claude_rules.md`
- General coding behavior and response formatting
- Code quality standards
- Communication guidelines

### 2. WordPress.org Plugin Submission Guide
**Location:** `.claude/docs/WordPress-Plugin-Submission-Complete-Guide.md`
- WordPress.org directory requirements
- Plugin header standards
- Security requirements
- Internationalization (i18n) requirements
- Readme.txt formatting

### 3. CodeCanyon Plugin Submission Guide
**Location:** `.claude/docs/codecanyon-plugin-submission-guide.md`
- Envato marketplace requirements
- Premium plugin standards
- File organization requirements
- Presentation and documentation requirements
- Revenue and licensing information

---

## Automatic Rules (Always Apply)

### Prefixing Requirements
- **ALL functions** must use unique prefix: `{plugin_slug}_`
- **ALL classes** must use unique prefix: `{Plugin_Name}_`
- **ALL hooks** must use unique prefix
- **ALL database options** must use unique prefix
- **ALL script/style handles** must use unique prefix
- Minimum prefix length: 3 characters (recommended: 5+)
- NEVER use `wp_` prefix (reserved for WordPress core)

### Security (Non-Negotiable)
```php
// ALWAYS sanitize input
$clean = sanitize_text_field( $_POST['field'] );

// ALWAYS escape output
echo esc_html( $variable );
echo esc_attr( $attribute );
echo esc_url( $url );

// ALWAYS use nonces for forms
wp_nonce_field( 'action_name', 'nonce_name' );

// ALWAYS verify nonces
if ( ! wp_verify_nonce( $_POST['nonce'], 'action' ) ) {
    wp_die( 'Security check failed' );
}

// ALWAYS check capabilities
if ( ! current_user_can( 'manage_options' ) ) {
    wp_die( 'Unauthorized' );
}

// ALWAYS use prepared statements
$wpdb->prepare( "SELECT * FROM table WHERE id = %d", $id );
```

### File Naming Convention
- Lowercase only
- Words separated by hyphens (NOT underscores)
- Example: `class-plugin-name-admin.php`

### Folder Structure (Required)
```
plugin-name/
├── plugin-name.php
├── uninstall.php
├── readme.txt
├── includes/
├── admin/
│   ├── css/
│   ├── js/
│   └── partials/
├── public/
│   ├── css/
│   ├── js/
│   └── partials/
├── languages/
└── assets/
```

### Code Standards
- Use TABS for indentation (not spaces)
- Opening brace on same line as function
- Use strict equality (`===`) not abstract (`==`)
- No PHP errors with WP_DEBUG enabled
- No deprecated functions
- No `eval()` or `create_function()`

### Asset Loading
```php
// CORRECT - Always use WordPress functions
wp_enqueue_script( 'handle', $url, array('jquery'), $ver, true );
wp_enqueue_style( 'handle', $url, array(), $ver );

// NEVER deregister default jQuery
// NEVER load duplicate core scripts
```

### Internationalization (i18n)
- ALL user-facing strings must be translatable
- Use consistent text domain matching plugin slug
- Include `.pot` file in `/languages/` folder

```php
// Correct i18n usage
__( 'Text', 'plugin-text-domain' );
_e( 'Text', 'plugin-text-domain' );
esc_html__( 'Text', 'plugin-text-domain' );
```

---

## When Creating New Plugins

1. **Ask for plugin name/slug first** if not provided
2. **Generate complete file structure** following the folder hierarchy above
3. **Include all required files:**
   - Main plugin file with proper header
   - `readme.txt` (WordPress.org format)
   - `uninstall.php` for cleanup
   - Documentation stub

4. **Apply all security measures** from the start
5. **Use proper prefixing** throughout

---

## When Reviewing/Fixing Code

1. Check for missing prefixes
2. Verify all output is escaped
3. Verify all input is sanitized
4. Check nonce implementation
5. Verify capability checks
6. Check for deprecated functions
7. Ensure proper asset loading
8. Verify i18n implementation

---

## Quick Reference Commands

When I say:
- **"Create plugin [name]"** → Generate complete plugin structure following all guidelines
- **"Review for submission"** → Check code against WordPress.org AND CodeCanyon requirements
- **"Fix security"** → Add missing sanitization, escaping, nonces, capability checks
- **"Add i18n"** → Make all strings translatable
- **"Prepare for CodeCanyon"** → Ensure all Envato marketplace requirements are met

---

## Do NOT:
- ❌ Use generic function names without prefix
- ❌ Output unescaped data
- ❌ Process input without sanitization
- ❌ Skip nonce verification
- ❌ Use direct database queries without prepare()
- ❌ Deregister WordPress default scripts
- ❌ Use inline CSS/JS
- ❌ Use deprecated functions
- ❌ Create files in plugin root (use folders)
- ❌ Use `wp_` prefix for custom functions

---

## References

For detailed information, read the full documentation in `.claude/docs/`:
- `claude_rules.md` - General AI behavior rules
- `WordPress-Plugin-Submission-Complete-Guide.md` - WordPress.org requirements
- `codecanyon-plugin-submission-guide.md` - CodeCanyon/Envato requirements

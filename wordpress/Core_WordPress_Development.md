# Skill: Core WordPress Development

## Purpose
To build, customize, and maintain WordPress websites using core best practices, including theme development, plugin development, hooks, and security.

## When to Use
- Building custom WordPress themes
- Creating custom plugins
- Modifying existing WordPress sites
- Optimizing WordPress performance
- Securing WordPress installations

## Procedure

### 1. Theme Development
Use child themes to customize existing themes safely:
```php
// style.css in child theme
/*
Theme Name:   My Child Theme
Template:     twentytwentyfour
Version:      1.0
*/
```
- Use `functions.php` to enqueue scripts/styles
- Follow WordPress template hierarchy (`index.php`, `single.php`, `page.php`, `archive.php`, etc.)
- Use `get_header()`, `get_footer()`, `get_sidebar()` for reusable parts

### 2. Plugin Development
Create custom plugins for site functionality:
```php
<?php
/**
 * Plugin Name: My Custom Plugin
 * Plugin URI: https://example.com
 * Description: Custom plugin for my site
 * Version: 1.0
 * Author: Your Name
 */

// Plugin code here
```
- Use hooks (actions & filters) to modify WordPress behavior
- Never edit core files!

### 3. Hooks System
**Actions**:
```php
// Add custom function to init hook
add_action('init', 'my_custom_function');

function my_custom_function() {
    // Code here
}
```
**Filters**:
```php
// Modify post content
add_filter('the_content', 'my_content_filter');

function my_content_filter($content) {
    return $content . '<p>Thank you for reading!</p>';
}
```

### 4. Security Best Practices
- Keep WordPress, themes, and plugins updated
- Use strong passwords
- Limit login attempts
- Use SSL/HTTPS
- Disable file editing in admin (`define('DISALLOW_FILE_EDIT', true);`)
- Sanitize and escape all user input:
  ```php
  $safe_input = sanitize_text_field($_POST['input']);
  echo esc_html($safe_output);
  ```

### 5. Performance Optimization
- Use caching plugins (WP Rocket, W3 Total Cache)
- Optimize images (Smush, ShortPixel)
- Use a CDN
- Keep plugins minimal
- Optimize database (WP-Optimize)

## Constraints
- Always use child themes instead of modifying parent themes directly
- Never modify WordPress core files
- Follow WordPress Coding Standards (https://developer.wordpress.org/coding-standards/)
- Test plugins/themes on a staging site before deploying to production

## Expected Output
A secure, performant, and maintainable WordPress website built with core best practices.

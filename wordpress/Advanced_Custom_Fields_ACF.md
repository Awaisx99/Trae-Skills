# Skill: Advanced Custom Fields (ACF)

## Purpose
To add custom content fields to WordPress posts, pages, custom post types, and more, enabling highly customized content structures.

## When to Use
- Adding custom fields to posts/pages
- Creating custom post types with custom fields
- Building options pages for site-wide settings
- Using repeaters, flexible content, and galleries
- Integrating ACF with Elementor/WooCommerce

## Procedure

### 1. Basic Field Creation
- Create field groups in ACF admin
- Add field types (text, textarea, image, select, checkbox, etc.)
- Set field group location rules (which post types/pages they appear on)

### 2. Displaying Fields in Themes
Get field values with `get_field()`:
```php
// Get a text field
$custom_text = get_field('custom_text_field');
echo $custom_text;

// Get an image field (array)
$image = get_field('custom_image');
echo '<img src="' . esc_url($image['url']) . '" alt="' . esc_attr($image['alt']) . '">';

// Get a repeater field
if (have_rows('repeater_field')) {
    while (have_rows('repeater_field')) {
        the_row();
        $sub_field = get_sub_field('sub_field');
        echo $sub_field;
    }
}
```
Or use shortcodes in posts: `[acf field="custom_field_name"]`

### 3. Options Pages
Create site-wide options pages:
```php
// In functions.php
if (function_exists('acf_add_options_page')) {
    acf_add_options_page([
        'page_title' => 'Site Settings',
        'menu_title' => 'Site Settings',
        'menu_slug' => 'site-settings',
        'capability' => 'edit_posts',
        'redirect' => false
    ]);
}
```
Get options fields: `get_field('footer_text', 'option');`

### 4. Advanced Fields
- **Repeater**: Repeatable sets of sub-fields
- **Flexible Content**: Layout builder with multiple layouts
- **Gallery**: Multiple image uploads
- **Relationship**: Connect posts/pages
- **Google Map**: Interactive maps

### 5. Integrations
- **Elementor**: Use ACF fields in Elementor widgets (Dynamic Tags)
- **WooCommerce**: Add custom fields to products
- **Gravity Forms**: Connect forms to ACF

## Constraints
- Always escape output when displaying ACF fields
- Use field keys instead of field names in code for reliability
- Follow ACF Documentation (https://www.advancedcustomfields.com/resources/)
- Keep fields organized into logical groups

## Expected Output
Highly customized WordPress content structures with easy-to-use custom fields.

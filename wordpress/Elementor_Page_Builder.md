# Skill: Elementor Page Builder

## Purpose
To create custom, responsive WordPress page layouts using the Elementor page builder, including custom widgets, templates, and advanced features.

## When to Use
- Building custom page layouts
- Creating landing pages
- Designing homepages, about pages, etc.
- Building custom Elementor widgets
- Using Elementor Pro features

## Procedure

### 1. Basic Layout Building
- Use drag-and-drop to add widgets (Sections, Columns, Widgets)
- Choose from pre-made templates (Elementor Library)
- Customize widget settings (Content, Style, Advanced tabs)
- Use responsive controls for mobile/tablet/desktop views

### 2. Custom Widget Development
Create custom Elementor widgets:
```php
class My_Custom_Widget extends \Elementor\Widget_Base {
    public function get_name() { return 'my-custom-widget'; }
    public function get_title() { return 'My Custom Widget'; }
    public function get_icon() { return 'eicon-posts-ticker'; }
    public function get_categories() { return [ 'general' ]; }

    protected function register_controls() {
        // Add controls here
    }

    protected function render() {
        // Widget output here
        echo 'Hello from my custom widget!';
    }
}

// Register widget
add_action('elementor/widgets/register', function($widgets_manager) {
    $widgets_manager->register(new \My_Custom_Widget());
});
```

### 3. Elementor Pro Features
- Use Theme Builder for headers/footers/single post templates
- Use Forms for contact forms, lead capture
- Use Dynamic Tags for dynamic content
- Use Popups for marketing
- Use WooCommerce Builder for shop pages

### 4. Performance Best Practices
- Use only necessary widgets
- Optimize images in Elementor
- Use Elementor's built-in performance settings
- Avoid too many nested sections/columns

## Constraints
- Always test Elementor designs on mobile devices
- Use Elementor's responsive controls instead of custom CSS when possible
- Keep custom widgets lightweight
- Follow Elementor Developer Guidelines (https://developers.elementor.com/)

## Expected Output
Beautiful, responsive, and performant WordPress page layouts built with Elementor.

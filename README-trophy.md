# Trophy Bootstrap Theme

A complete Bootstrap theme inspired by the Trophy soccer club website, featuring custom typography, clean minimal button styles, and a sophisticated color palette.

## Features

### Typography
- **Font Families**: Titillium Web (primary) and Fira Sans (secondary)
- **Heading Sizes**: Based on Trophy's exact typography scale (H1: 60px, H2: 36px, H3: 25px, etc.)
- **Responsive Typography**: Automatically scales on mobile devices
- **Custom Typography Classes**: Additional styling options for enhanced control
- **Professional Typography**: Clean, readable text with proper spacing and weights

### Button Styles
- **Minimal Buttons**: Clean text-only buttons with subtle hover effects
- **Outline Buttons**: Bordered buttons that fill on hover
- **Solid Buttons**: Filled buttons with smooth transitions

### Button Sizes
- Small (`.btn-sm`)
- Medium (default)
- Large (`.btn-lg`)

### Color Palette
- **Primary**: Trophy Green (#43ec6b) - The signature Trophy color
- **Secondary**: Turquoise (#3cefd2) - Modern accent color
- **Accent**: Black (#000000) - Professional and bold
- **Dark**: Charcoal (#221f1b) - Sophisticated dark tone
- **Gray**: Medium Gray (#5c5a5b) - For secondary text

### Key Design Elements
- Sharp corners (border-radius: 0) for modern look
- Professional typography matching Trophy's design
- Smooth hover animations with subtle effects
- Clean, minimal aesthetic inspired by Trophy soccer club
- Complete Bootstrap 5 integration

## Installation

1. Include the compiled CSS file:
```html
<link href="dist/css/bootstrap-trophy.css" rel="stylesheet">
```

2. Add Google Fonts for Typography:
```html
<link href="https://fonts.googleapis.com/css2?family=Titillium+Web:wght@200;300;400;600;700;900&family=Fira+Sans:wght@100;200;300;400;500;600;700;800;900&display=swap" rel="stylesheet">
```

## Usage Examples

### Typography

#### Headings
```html
<h1>Main Hero Heading (60px)</h1>
<h2>Section Heading (36px)</h2>
<h3>Subsection Heading (25px)</h3>
<h4>Content Heading (22px)</h4>
<h5>Small Heading (20px)</h5>
<h6>Tiny Heading (13px)</h6>
```

#### Special Typography Classes
```html
<h1 class="trophy-heading-hero">Large Hero Heading</h1>
<h2 class="trophy-heading-section">Section with Underline</h2>
<p class="trophy-text-primary">Primary colored text</p>
<p class="trophy-fw-bold trophy-fs-large">Bold and large text</p>
```

#### Text Utilities
```html
<!-- Color utilities -->
<p class="trophy-text-primary">Trophy green text</p>
<p class="trophy-text-secondary">Turquoise text</p>
<p class="trophy-text-accent">Black text</p>
<p class="trophy-text-gray">Gray text</p>

<!-- Font weight utilities -->
<p class="trophy-fw-light">Light weight</p>
<p class="trophy-fw-normal">Normal weight</p>
<p class="trophy-fw-medium">Medium weight</p>
<p class="trophy-fw-semibold">Semibold weight</p>
<p class="trophy-fw-bold">Bold weight</p>

<!-- Font size utilities -->
<p class="trophy-fs-small">Small text</p>
<p class="trophy-fs-normal">Normal text</p>
<p class="trophy-fs-large">Large text</p>
<p class="trophy-fs-xlarge">Extra large text</p>
```

### Buttons

#### Minimal Buttons
```html
<button class="btn trophy-btn-minimal">Minimal Button</button>
<button class="btn trophy-btn-minimal btn-sm">Small Minimal</button>
<button class="btn trophy-btn-minimal btn-lg">Large Minimal</button>
```

#### Outline Buttons
```html
<button class="btn trophy-btn-outline">Outline Button</button>
<button class="btn trophy-btn-outline btn-sm">Small Outline</button>
<button class="btn trophy-btn-outline btn-lg">Large Outline</button>
```

#### Solid Buttons
```html
<button class="btn trophy-btn-solid">Solid Button</button>
<button class="btn trophy-btn-solid btn-sm">Small Solid</button>
<button class="btn trophy-btn-solid btn-lg">Large Solid</button>
```

## Building from Source

If you want to customize the theme:

1. Install dependencies:
```bash
npm install
```

2. Build the CSS:
```bash
npm run build
```

3. Watch for changes during development:
```bash
npm run watch
```

4. Build both expanded and minified versions:
```bash
npm run build-all
```

## Customization

### Colors
Modify the color variables in `scss/_trophy-variables.scss`:

```scss
$trophy-primary: #43ec6b !default;        // Trophy green
$trophy-secondary: #3cefd2 !default;      // Turquoise
$trophy-accent: #000000 !default;         // Black
$trophy-dark: #221f1b !default;           // Charcoal
$trophy-gray: #5c5a5b !default;           // Medium gray
```

### Typography
Adjust font settings and sizes:

```scss
// Font families
$trophy-font-family-primary: 'Titillium Web', sans-serif !default;
$trophy-font-family-secondary: 'Fira Sans', sans-serif !default;

// Heading sizes (converted to rem)
$trophy-h1-font-size: 3.75rem !default;   // 60px
$trophy-h2-font-size: 2.25rem !default;   // 36px
$trophy-h3-font-size: 1.5625rem !default; // 25px
$trophy-h4-font-size: 1.375rem !default;  // 22px
$trophy-h5-font-size: 1.25rem !default;   // 20px
$trophy-h6-font-size: 0.8125rem !default; // 13px

// Base paragraph
$trophy-p-font-size: 0.9375rem !default;  // 15px
$trophy-p-line-height: 1.6 !default;

// Font weights
$trophy-font-weight-light: 300 !default;
$trophy-font-weight-normal: 400 !default;
$trophy-font-weight-medium: 500 !default;
$trophy-font-weight-semibold: 600 !default;
$trophy-font-weight-bold: 700 !default;
```

### Button Styles
Customize button appearance:

```scss
$trophy-btn-font-family: $trophy-font-family !default;
$trophy-btn-font-weight: $trophy-font-weight-semibold !default;
$trophy-btn-line-height: 1.2 !default;
$trophy-btn-border-radius: 0 !default;
$trophy-btn-border-width: 1px !default;
$trophy-btn-transition: all 0.3s ease-in-out !default;
```

## File Structure

```
scss/
├── _trophy-variables.scss     # Theme variables, colors, and typography
├── _trophy-typography.scss    # Typography styles and text utilities  
├── _trophy-buttons.scss       # Button mixins and custom styles
└── bootstrap-trophy.scss      # Main theme file that imports everything

dist/
├── css/
│   ├── bootstrap-trophy.css     # Expanded CSS build
│   └── bootstrap-trophy.min.css # Minified CSS build

trophy-complete-demo.html     # Complete demonstration with typography and buttons
trophy-theme-demo.html        # Original button-focused demo
```

## Browser Support

This theme supports all modern browsers that support CSS3 transitions and transforms:
- Chrome 60+
- Firefox 60+
- Safari 12+
- Edge 79+

## Inspiration

This theme is inspired by the Trophy soccer club website, which features:
- Clean, minimal design aesthetic with Titillium Web and Fira Sans typography
- Professional sports branding with Trophy green (#43ec6b) as the primary color
- Exact typography scale matching the original design (60px, 36px, 25px, etc.)
- Modern button styles with smooth hover effects
- Sharp, contemporary styling with zero border radius
- Responsive design that works across all devices

## License

MIT License - feel free to use in personal and commercial projects.

## Demo

- `trophy-complete-demo.html` - Complete demonstration of typography, buttons, colors, and all theme features
- `trophy-theme-demo.html` - Original button-focused demonstration

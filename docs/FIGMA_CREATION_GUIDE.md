# Figma Wireframe Creation Guide for Agora

This guide provides step-by-step instructions for creating Figma wireframes from the specifications in `doc/WIREFRAME_SPECIFICATIONS.md`.

---

## Prerequisites

- Figma Desktop or Figma Web access
- Basic familiarity with Figma tools (frames, auto-layout, components)
- Reference to `doc/WIREFRAME_SPECIFICATIONS.md` for detailed measurements

---

## Step 1: Set Up Your Figma File

### 1.1 Create New File

1. Open Figma and create a new file
2. Name it: `Agora - Wireframes`

### 1.2 Create Pages

Create three pages:

- `01 - Question Submission`
- `02 - Debate Viewing`
- `03 - Philosopher Selection`

### 1.3 Set Up Frames

For each page, create frames for different breakpoints:

**Mobile Frame:**

- Name: `Mobile - [Screen Name]`
- Width: `375px`
- Height: `812px`
- Frame type: Phone

**Tablet Frame:**

- Name: `Tablet - [Screen Name]`
- Width: `768px`
- Height: `1024px`
- Frame type: Tablet

**Desktop Frame:**

- Name: `Desktop - [Screen Name]`
- Width: `1440px`
- Height: `900px`
- Frame type: Desktop

---

## Step 2: Create Design System

### 2.1 Color Styles

Create color styles matching the palette from specifications:

**Primary Colors:**

- `Primary` → `#1E3A5F`
- `Primary Variant` → `#2D4A6F`
- `Secondary` → `#6B7280`
- `Secondary Variant` → `#9CA3AF`
- `Accent` → `#D4AF37`
- `Error` → `#DC2626`

**Surface Colors:**

- `Surface` → `#FFFFFF`
- `Surface Variant` → `#F5F5F5`
- `Surface Container` → `#E5E5E5`
- `Background` → `#FAFAFA`

**Text Colors:**

- `On Surface` → `#1A1A1A`
- `On Surface Variant` → `#6B7280`
- `On Primary` → `#FFFFFF`
- `On Secondary` → `#FFFFFF`

**Philosopher Colors:**

- `Philosopher Blue` → `#3B82F6`
- `Philosopher Purple` → `#8B5CF6`
- `Philosopher Pink` → `#EC4899`
- `Philosopher Green` → `#10B981`
- `Philosopher Orange` → `#F59E0B`
- `Philosopher Teal` → `#14B8A6`
- `Philosopher Indigo` → `#6366F1`

**How to Create:**

1. Select any shape
2. Open the Fill color picker
3. Enter hex value
4. Click the "Style" icon (4 dots) next to the color
5. Click "+" to create new style
6. Name the style (e.g., "Primary")

### 2.2 Text Styles

Create text styles for each typography scale:

**Display:**

- `Display Large` → 57px, Line height: 64px, Weight: Regular
- `Display Small` → 36px, Line height: 44px, Weight: Regular

**Headline:**

- `Headline Medium` → 28px, Line height: 36px, Weight: Regular

**Title:**

- `Title Large` → 22px, Line height: 28px, Weight: Medium
- `Title Medium` → 16px, Line height: 24px, Weight: Medium
- `Title Small` → 14px, Line height: 20px, Weight: Medium

**Body:**

- `Body Large` → 16px, Line height: 24px, Weight: Regular
- `Body Medium` → 14px, Line height: 20px, Weight: Regular
- `Body Small` → 12px, Line height: 16px, Weight: Regular

**Label:**

- `Label Large` → 14px, Line height: 20px, Weight: Medium
- `Label Medium` → 12px, Line height: 16px, Weight: Medium
- `Label Small` → 11px, Line height: 16px, Weight: Medium

**How to Create:**

1. Select text layer
2. Set font, size, line height, weight
3. Click "Style" icon (4 dots) in Text section
4. Click "+" to create new style
5. Name the style

### 2.3 Spacing Tokens

Create a reference frame with spacing guides:

1. Create a frame named `Spacing Reference`
2. Add rectangles with these widths/heights:
   - `4px` (space4)
   - `8px` (space8)
   - `12px` (space12)
   - `16px` (space16)
   - `24px` (space24)
   - `32px` (space32)
   - `40px` (space40)
   - `48px` (space48)
3. Label each rectangle
4. Use these as reference when building components

---

## Step 3: Create Component Library

### 3.1 TextField Component

**Create Base Component:**

1. Create a frame: `TextField - Outlined`
2. Width: `100%` (will be constrained by parent)
3. Height: `56px` (single line) or `72px` (multi-line)

**Structure:**

- **Label** (above field):
  - Text: "Label"
  - Style: `Body Medium`
  - Color: `On Surface`
  - Position: Top, `4px` padding below

- **Field Container**:
  - Rectangle with:
    - Border: `1px` solid `#E5E5E5`
    - Border radius: `4px`
    - Fill: `Surface`
    - Padding: `16px` internal

- **Input Text** (placeholder):
  - Text: "Enter text..."
  - Style: `Body Large`
  - Color: `On Surface Variant`
  - Position: Inside field container

- **Helper Text** (below field):
  - Text: "Helper text"
  - Style: `Body Small`
  - Color: `On Surface Variant`
  - Position: Bottom, `4px` padding above

**Create Variants:**

- Default
- Focused (border: `2px` solid `Primary`)
- Error (border: `2px` solid `Error`, error text visible)
- Disabled (opacity: 60%)

**Auto-layout Setup:**

- Set frame to vertical auto-layout
- Spacing: `4px` between elements
- Padding: `0px` (handled by internal elements)

### 3.2 Button Component

**Create Base Component:**

1. Create a frame: `Button - Filled`
2. Height: `40px`
3. Min width: `200px`

**Structure:**

- **Button Container**:
  - Rectangle with:
    - Fill: `Primary`
    - Border radius: `20px`
    - Shadow: `1dp` elevation (use Figma's shadow: Y: 1px, Blur: 2px, Color: black 20% opacity)

- **Button Text**:
  - Text: "Button"
  - Style: `Label Large`
  - Color: `On Primary`
  - Centered horizontally and vertically

**Create Variants:**

- Default
- Hover (elevation: `2dp`)
- Pressed (elevation: `0dp`)
- Disabled (fill: `Surface Container`, text: `Secondary Variant`, no shadow)

**Auto-layout Setup:**

- Horizontal auto-layout
- Padding: `24px` horizontal, `0px` vertical
- Alignment: Center

**Create Text Button Variant:**

- Same structure but:
  - No background fill
  - Text color: `Primary`
  - Padding: `12px` horizontal

### 3.3 Card Component

**Create Base Component:**

1. Create a frame: `Card`
2. Border radius: `12px`
3. Fill: `Surface`

**Structure:**

- **Card Container**:
  - Frame with:
    - Fill: `Surface`
    - Border radius: `12px`
    - Shadow: `1dp` elevation
    - Padding: `16px` all sides

**Create Variants:**

- Default (elevation: `1dp`)
- Selected (elevation: `4dp`, border: `2px` solid `Primary`)
- Action Bar (elevation: `8dp`)

**Auto-layout Setup:**

- Vertical auto-layout
- Padding: `16px`
- Fill container: Yes

### 3.4 Chip Component

**Create Base Component:**

1. Create a frame: `Chip - Assist`
2. Height: `32px`
3. Border radius: `8px`

**Structure:**

- **Chip Container**:
  - Frame with:
    - Fill: `Surface Variant` (or philosopher color at 20% opacity)
    - Border radius: `8px`
    - Padding: `12px` horizontal

- **Chip Text**:
  - Text: "Chip"
  - Style: `Label Medium`
  - Color: `On Surface` (or philosopher color)

**Auto-layout Setup:**

- Horizontal auto-layout
- Padding: `12px` horizontal, `0px` vertical
- Alignment: Center

### 3.5 Philosopher Card Component

**Create Base Component:**

1. Create a frame: `Philosopher Card - Selectable`
2. Width: `140px` (mobile) or `160px` (desktop)
3. Height: `120px`

**Structure:**

- **Card Container** (from Card component):
  - Border: `2px` solid transparent (default)
  - Border: `2px` solid `Primary` (selected)

- **Content** (vertical stack):
  - **Avatar**: `48px` × `48px` circle
  - **Name**: `Body Large`, centered
  - **Tradition Chip**: `Chip - Assist` component
  - **Selection Indicator**: Checkmark icon (visible when selected)

**Create Variants:**

- Default
- Selected (border, elevation, background change)

**Auto-layout Setup:**

- Vertical auto-layout
- Spacing: `8px`
- Alignment: Center
- Padding: `16px`

---

## Step 4: Build Screen 1 - Question Submission

### 4.1 Set Up Frame

1. Select the mobile frame for this screen
2. Set background color to `Background` (#FAFAFA)

### 4.2 Create Container

1. Create a frame: `Content Container`
2. Width: Full width (mobile) or `600px` max (desktop)
3. Padding: `24px` all sides
4. Auto-layout: Vertical
5. Alignment: Center (horizontal)

### 4.3 Add App Header

1. Create a frame: `App Header`
2. Auto-layout: Vertical
3. Alignment: Center
4. Spacing: `32px` below title

**Title:**

- Text: "Agora"
- Style: `Display Large`
- Color: `On Surface`

**Subtitle:**

- Text: "Pose a question. Witness the debate."
- Style: `Body Medium`
- Color: `On Surface Variant`
- Spacing: `24px` below

### 4.4 Add Question Input Field

1. Use `TextField - Outlined` component
2. Label: "Your Question"
3. Helper text: "10-500 characters"
4. Add character counter (right-aligned, `Body Small`, `On Surface Variant`)
5. Spacing: `24px` below

### 4.5 Add Context Field

1. Use `TextField - Outlined` component
2. Label: "Additional Context (Optional)"
3. Helper text: "Provide background or context for your question"
4. Spacing: `24px` below

### 4.6 Add Philosopher Selection Section

1. Create a frame: `Philosopher Selection`
2. Auto-layout: Vertical
3. Spacing: `16px` below header

**Section Header:**

- Text: "Select Philosophers"
- Style: `Title Medium`
- Color: `On Surface`
- Spacing: `16px` below

**Philosopher Cards:**

1. Create horizontal scroll frame (mobile) or grid (desktop)
2. Use `Philosopher Card - Selectable` components
3. Spacing: `16px` between cards
4. Show 2-4 philosopher cards as examples

### 4.7 Add Submit Button

1. Use `Button - Filled` component
2. Text: "Start Debate"
3. Width: Full width (mobile) or auto (desktop)
4. Spacing: `32px` above

### 4.8 Create State Variants

Create separate frames or use component variants for:

- Default state
- Loading state (button shows loading indicator)
- Error state (error text below fields)

---

## Step 5: Build Screen 2 - Debate Viewing

### 5.1 Set Up Frame

1. Select the mobile frame
2. Set background color to `Background`

### 5.2 Create Sticky Header

1. Create a frame: `Sticky Header`
2. Background: `Surface`
3. Padding: `16px` all sides
4. Min height: `80px`
5. Position: Fixed at top (use constraints)

**Content:**

- **Question Text**: `Title Large`, `On Surface`
- **New Question Button**: `Button - Text`, top-right

### 5.3 Create Debate Timeline

1. Create a frame: `Debate Timeline`
2. Auto-layout: Vertical
3. Spacing: `16px` between cards
4. Padding: `16px` horizontal, `24px` vertical

### 5.4 Create Argument Cards

1. Use `Card` component as base
2. Add left border accent (`4px` solid philosopher color)
3. Structure:
   - **Header Row** (horizontal auto-layout):
     - Avatar (`40px` circle)
     - Name (`Title Medium`)
     - Tradition Chip (`Chip - Assist`)
     - Timestamp (`Label Small`, `On Surface Variant`, right-aligned)
   - **Argument Text** (`Body Large`, `On Surface`)
   - **Streaming Indicator** (optional, animated dots)

4. Create 2-3 example argument cards with different philosophers

### 5.5 Create Thinking Indicator

1. Use `Card` component (elevation: `0dp`)
2. Background: `Surface Container`
3. Content:
   - Progress indicator (`20px` circle)
   - Text: "{Name} is thinking..." (`Body Medium`, italic, `On Surface Variant`)

### 5.6 Create Empty State

1. Centered frame
2. Loading indicator (`40px` circle)
3. Text: "Debate starting..." (`Body Large`, `On Surface Variant`)

---

## Step 6: Build Screen 3 - Philosopher Selection

### 6.1 Set Up Frame

1. Select the mobile frame
2. Set background color to `Background`

### 6.2 Create Screen Header

1. Create a frame: `Screen Header`
2. Auto-layout: Vertical
3. Spacing: `8px` between title and subtitle

**Title:**

- Text: "Choose Philosophers"
- Style: `Display Small`
- Color: `On Surface`

**Subtitle:**

- Text: "Select 2 philosophers for the debate"
- Style: `Body Medium`
- Color: `On Surface Variant`
- Spacing: `24px` below

### 6.3 Create Philosopher Grid

1. Create a frame: `Philosopher Grid`
2. Use Grid layout (2 columns mobile, 3-4 desktop)
3. Spacing: `16px` both axes

### 6.4 Create Philosopher Cards

1. Use `Card` component as base
2. Structure (vertical auto-layout, centered):
   - Avatar (`64px` circle)
   - Name (`Title Medium`)
   - Tradition Chip (`Chip - Assist`)
   - Description (`Body Small`, 2-3 lines, centered)
   - Selection indicator (checkmark, top-right when selected)

3. Create 6-7 example philosopher cards
4. Show 2 in selected state

### 6.5 Create Action Bar

1. Create a frame: `Action Bar`
2. Position: Fixed at bottom (use constraints)
3. Background: `Surface`
4. Elevation: `8dp` shadow
5. Border top: `1px` solid `#E5E5E5`
6. Padding: `16px` all sides

**Content** (horizontal auto-layout):

- Selection count: "{X} selected" (`Body Medium`, `On Surface Variant`)
- Start Debate button: `Button - Filled`, full width

---

## Step 7: Create Responsive Variants

### 7.1 Duplicate Frames

1. For each screen, duplicate the mobile frame
2. Rename for tablet and desktop
3. Adjust dimensions

### 7.2 Adjust Layouts

- **Question Submission**: Center content, max width `600px`
- **Philosopher Selection**: Increase grid columns (3 tablet, 4 desktop)
- **Debate Viewing**: Increase max content width, adjust card sizes

### 7.3 Test Breakpoints

1. Use Figma's responsive resize feature
2. Ensure components adapt correctly
3. Adjust spacing and sizing as needed

---

## Step 8: Add Annotations

### 8.1 Add Measurement Annotations

1. Use Figma's measurement tool or create annotation frames
2. Label key measurements:
   - Spacing between elements
   - Component dimensions
   - Padding values

### 8.2 Add State Labels

1. Create text labels for different states
2. Use a consistent annotation style
3. Group annotations separately from wireframes

### 8.3 Add Interaction Notes

1. Add notes for:
   - Hover states
   - Click interactions
   - Loading states
   - Error states

---

## Step 9: Organize and Export

### 9.1 Organize Layers

1. Use clear layer naming conventions:
   - `[Component Name] - [State]`
   - `[Section Name] - [Breakpoint]`
2. Group related elements
3. Use frames for logical sections

### 9.2 Create Component Library Page

1. Create a new page: `00 - Component Library`
2. Place all reusable components here
3. Organize by category (Buttons, Cards, Inputs, etc.)

### 9.3 Export Settings

1. Set up export settings for screenshots
2. Recommended formats:
   - PNG for presentations (2x resolution)
   - PDF for documentation
   - SVG for vector graphics

---

## Naming Conventions

### Components

- `[Component Type] - [Variant]`
- Example: `Button - Filled`, `Card - Selected`

### Frames

- `[Breakpoint] - [Screen Name]`
- Example: `Mobile - Question Submission`

### Layers

- `[Element Type] - [Description]`
- Example: `Text - Title`, `Frame - Container`

---

## Tips and Best Practices

1. **Use Auto-layout**: Makes components responsive and easier to maintain
2. **Create Variants**: Use component variants for states (default, selected, disabled)
3. **Consistent Spacing**: Always use spacing tokens (4px, 8px, 16px, etc.)
4. **Color Styles**: Use color styles, not direct hex values
5. **Text Styles**: Use text styles for all typography
6. **Component Nesting**: Build complex components from simpler ones
7. **Constraints**: Use constraints for responsive behavior
8. **Frames vs Groups**: Use frames for layout, groups for organization
9. **Naming**: Be consistent and descriptive
10. **Documentation**: Add notes and annotations for clarity

---

## Next Steps

After creating wireframes:

1. Review with stakeholders
2. Iterate based on feedback
3. Create high-fidelity designs (if needed)
4. Hand off to developers with specifications document
5. Maintain component library as design system evolves

---

## Resources

- [Figma Auto Layout Guide](https://help.figma.com/hc/en-us/articles/5731389357079)
- [Figma Component Variants](https://help.figma.com/hc/en-us/articles/5579474822679)
- [Figma Constraints](https://help.figma.com/hc/en-us/articles/360039956914)
- Flutter Material Design 3: [material.io/design](https://material.io/design)

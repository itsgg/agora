# Agora - Figma Wireframe Specifications

## Overview

This document provides comprehensive wireframe specifications for three main screens of the Agora application, aligned with Flutter Material Design 3 (M3) components and the minimalist, philosophical aesthetic outlined in the project specification.

---

## Flutter Material Design 3 Reference

### Typography Scale

| Style | Font Size | Line Height | Usage |
|-------|-----------|-------------|-------|
| `displayLarge` | 57px | 64px | App title, hero text |
| `displayMedium` | 45px | 52px | Large screen titles |
| `displaySmall` | 36px | 44px | Screen titles |
| `headlineLarge` | 32px | 40px | Section headers |
| `headlineMedium` | 28px | 36px | Subsection headers |
| `headlineSmall` | 24px | 32px | Card titles |
| `titleLarge` | 22px | 28px | Question display, important labels |
| `titleMedium` | 16px | 24px | Philosopher names, section headers |
| `titleSmall` | 14px | 20px | Secondary labels |
| `bodyLarge` | 16px | 24px | Argument text, primary content |
| `bodyMedium` | 14px | 20px | Descriptions, helper text, button labels |
| `bodySmall` | 12px | 16px | Philosopher descriptions, metadata |
| `labelLarge` | 14px | 20px | Button labels, emphasized text |
| `labelMedium` | 12px | 16px | Chips, badges, secondary labels |
| `labelSmall` | 11px | 16px | Timestamps, captions |

### Spacing System (4dp Grid)

| Token | Value | Usage |
|-------|-------|-------|
| `space4` | 4px | Tight spacing, icon padding |
| `space8` | 8px | Compact spacing, small gaps |
| `space12` | 12px | Medium-tight spacing |
| `space16` | 16px | Standard spacing, component padding |
| `space24` | 24px | Comfortable spacing, section gaps |
| `space32` | 32px | Generous spacing, major sections |
| `space40` | 40px | Large section separation |
| `space48` | 48px | Extra large spacing |

### Color System

#### Primary Palette (Philosophical/Minimalist)

| Role | Hex | Usage |
|------|-----|-------|
| Primary | `#1E3A5F` | Primary actions, accents |
| Primary Variant | `#2D4A6F` | Hover states, pressed |
| Secondary | `#6B7280` | Secondary actions, icons |
| Secondary Variant | `#9CA3AF` | Disabled states |
| Accent | `#D4AF37` | Highlights, emphasis |
| Error | `#DC2626` | Error states, validation |

#### Surface Colors

| Role | Hex | Usage |
|------|-----|-------|
| Surface | `#FFFFFF` | Card backgrounds, main surface |
| Surface Variant | `#F5F5F5` | Alternate card backgrounds |
| Surface Container | `#E5E5E5` | Thinking indicators, subtle backgrounds |
| Background | `#FAFAFA` | App background |

#### Text Colors

| Role | Hex | Usage |
|------|-----|-------|
| On Surface | `#1A1A1A` | Primary text |
| On Surface Variant | `#6B7280` | Secondary text, helper text |
| On Primary | `#FFFFFF` | Text on primary buttons |
| On Secondary | `#FFFFFF` | Text on secondary elements |

#### Philosopher Color Palette

Each philosopher should have a distinct color for visual identification:

| Philosopher | Color | Hex |
|-------------|-------|-----|
| Philosopher 1 | Blue | `#3B82F6` |
| Philosopher 2 | Purple | `#8B5CF6` |
| Philosopher 3 | Pink | `#EC4899` |
| Philosopher 4 | Green | `#10B981` |
| Philosopher 5 | Orange | `#F59E0B` |
| Philosopher 6 | Teal | `#14B8A6` |
| Philosopher 7 | Indigo | `#6366F1` |

### Component Specifications

#### TextField (Outlined)

- Border radius: `4px`
- Border width: `1px` (default), `2px` (focused)
- Padding: `16px` internal
- Label padding: `4px` above field
- Helper text padding: `4px` below field
- Min height: `56px` (single line), `72px` (multi-line)

#### Card

- Border radius: `12px`
- Elevation: `1dp` (default), `4dp` (selected), `8dp` (action bar)
- Padding: `16px` standard
- Surface tint: `4%` opacity of primary color

#### Button (Filled)

- Border radius: `20px` (rounded)
- Min height: `40px`
- Horizontal padding: `24px`
- Typography: `labelLarge` (14px/20px)
- Elevation: `1dp` (default), `0dp` (pressed)

#### Button (Text)

- Border radius: `20px`
- Min height: `40px`
- Horizontal padding: `12px`
- Typography: `labelLarge`

#### Chip (Assist/Filter)

- Border radius: `8px`
- Height: `32px`
- Horizontal padding: `12px`
- Typography: `labelMedium` (12px/16px)

---

## Screen 1: Question Submission Screen

### Layout Structure

- **Container**: Vertical column layout, centered content
- **Max width**: `600px` (desktop), full width (mobile)
- **Padding**: `24px` on all sides
- **Background**: `#FAFAFA` (Background color)

### Component Breakdown

#### 1. App Header

**Specifications:**

- **Title**: "Agora"
  - Typography: `displayLarge` (57px/64px)
  - Color: `#1A1A1A` (On Surface)
  - Alignment: Center
  - Spacing: `32px` below

- **Subtitle**: "Pose a question. Witness the debate."
  - Typography: `bodyMedium` (14px/20px)
  - Color: `#6B7280` (On Surface Variant)
  - Alignment: Center
  - Spacing: `24px` below

**Measurements:**

- Total header height: ~`120px` (including spacing)

#### 2. Question Input Field

**Component**: M3 OutlinedTextField

**Specifications:**

- **Label**: "Your Question"
  - Typography: `bodyMedium` (14px/20px)
  - Color: `#1A1A1A` (On Surface)
  - Position: Above field, `4px` padding

- **Field**:
  - Typography: `bodyLarge` (16px/24px) for input text
  - Min height: `72px` (multi-line, ~3 lines visible)
  - Max height: `200px` (scrollable if exceeded)
  - Border: `1px` solid `#E5E5E5` (default)
  - Border (focused): `2px` solid `#1E3A5F` (Primary)
  - Border radius: `4px`
  - Internal padding: `16px`
  - Background: `#FFFFFF` (Surface)

- **Helper Text**: "10-500 characters"
  - Typography: `bodySmall` (12px/16px)
  - Color: `#6B7280` (On Surface Variant)
  - Position: Below field, `4px` padding

- **Character Counter**: Dynamic, right-aligned
  - Typography: `bodySmall` (12px/16px)
  - Color: `#6B7280` (default), `#DC2626` (error if < 10 or > 500)
  - Format: "X / 500"

**Spacing**: `24px` below

#### 3. Optional Context Field

**Component**: M3 OutlinedTextField

**Specifications:**

- **Label**: "Additional Context (Optional)"
  - Typography: `bodyMedium` (14px/20px)
  - Color: `#1A1A1A` (On Surface)
  - Position: Above field, `4px` padding

- **Field**:
  - Typography: `bodyLarge` (16px/24px)
  - Min height: `56px` (multi-line, ~2 lines visible)
  - Max height: `150px`
  - Border: `1px` solid `#E5E5E5`
  - Border (focused): `2px` solid `#1E3A5F`
  - Border radius: `4px`
  - Internal padding: `16px`
  - Background: `#FFFFFF`

- **Helper Text**: "Provide background or context for your question"
  - Typography: `bodySmall` (12px/16px)
  - Color: `#6B7280`
  - Position: Below field, `4px` padding

**Spacing**: `24px` below

#### 4. Philosopher Selection Section

**Section Header:**

- **Text**: "Select Philosophers"
  - Typography: `titleMedium` (16px/24px)
  - Color: `#1A1A1A` (On Surface)
  - Spacing: `16px` below

**Layout Options:**

#### Option A: Horizontal Scrollable List (Mobile)

- Scroll direction: Horizontal
- Item spacing: `16px`
- Padding: `0px` (no side padding, allows edge-to-edge scroll)

#### Option B: Grid Layout (Desktop)

- Columns: 3-4 (responsive)
- Grid spacing: `16px` (both axes)
- Max width: `600px` (matches container)

**Philosopher Card (Selectable):**

**Component**: Custom Card with M3 FilterChip styling

**Specifications:**

- **Card**:
  - Width: `140px` (mobile), `160px` (desktop)
  - Height: `120px`
  - Border radius: `12px`
  - Border: `2px` solid transparent (default), `2px` solid `#1E3A5F` (selected)
  - Background: `#FFFFFF` (default), `#F5F5F5` (selected)
  - Padding: `16px`
  - Elevation: `1dp` (default), `4dp` (selected)

- **Content** (vertical stack, centered):
  - **Avatar/Emoji**: `48px` × `48px`, centered
  - **Name**: Typography `bodyLarge` (16px/24px), centered, `8px` spacing below
  - **Tradition Badge**: M3 AssistChip
    - Typography: `labelMedium` (12px/16px)
    - Height: `24px`
    - Background: Philosopher color at 20% opacity
    - Text color: Philosopher color
    - `8px` spacing below
  - **Selection Indicator**: Checkmark icon (visible when selected)
    - Size: `24px` × `24px`
    - Color: `#1E3A5F` (Primary)
    - Position: Top-right corner, `8px` offset

**Spacing**: `16px` between cards, `24px` below section

#### 5. Submit Button

**Component**: M3 FilledButton

**Specifications:**

- **Text**: "Start Debate"
  - Typography: `labelLarge` (14px/20px)
  - Color: `#FFFFFF` (On Primary)

- **Button**:
  - Width: Full width (mobile), auto with min `200px` (desktop)
  - Height: `40px`
  - Border radius: `20px`
  - Background: `#1E3A5F` (Primary)
  - Background (disabled): `#E5E5E5` (Surface Container)
  - Text color (disabled): `#9CA3AF` (Secondary Variant)
  - Elevation: `1dp` (default), `0dp` (pressed)
  - Horizontal padding: `24px`

**Spacing**: `32px` above

**States:**

- **Default**: Enabled when question is valid (10-500 chars) and at least 2 philosophers selected
- **Loading**: Shows `CircularProgressIndicator` (size: `20px`, color: `#FFFFFF`)
- **Disabled**: When question invalid or < 2 philosophers selected

### Question Submission State Variations

#### Question Submission Default State

- Empty form
- All fields in default state
- Submit button disabled

#### Question Submission Validating State

- Character counter visible and updating
- Real-time validation feedback
- Submit button enabled/disabled based on validation

#### Question Submission Loading State

- Submit button shows loading indicator
- All inputs disabled
- Optional: Overlay with "Starting debate..." message

#### Question Submission Error State

- Error text below invalid field
  - Typography: `bodySmall` (12px/16px)
  - Color: `#DC2626` (Error)
- Field border color: `#DC2626`
- Submit button disabled

---

## Screen 2: Debate Viewing Interface

### Debate Viewing Layout Structure

- **Container**: Scrollable vertical list
- **Background**: `#FAFAFA` (Background)
- **Sticky header**: Fixed at top when scrolling
- **Content padding**: `16px` horizontal, `24px` vertical

### Debate Viewing Component Breakdown

#### 1. Sticky Header

**Component**: M3 Surface with elevation

**Specifications:**

- **Background**: `#FFFFFF` (Surface)
- **Elevation**: `0dp` (at top), `2dp` (when scrolled)
- **Padding**: `16px` all sides
- **Min height**: `80px`

**Content:**

- **Question Display**:
  - Typography: `titleLarge` (22px/28px)
  - Color: `#1A1A1A` (On Surface)
  - Max lines: 2 (ellipsis if exceeded)
  - Width: ~`80%` (leaves room for button)

- **New Question Button**:
  - Component: M3 TextButton
  - Text: "New Question"
  - Typography: `labelLarge` (14px/20px)
  - Color: `#1E3A5F` (Primary)
  - Position: Top-right
  - Padding: `12px` horizontal

**Spacing**: `16px` below header

#### 2. Debate Timeline

**Layout**: Vertical list (ListView)

**Specifications:**

- **Spacing**: `16px` between argument cards
- **Padding**: `16px` horizontal, `24px` top/bottom
- **Auto-scroll**: Automatically scrolls to latest argument

#### 3. Argument Card

**Component**: M3 Card

**Specifications:**

- **Card**:
  - Border radius: `12px`
  - Elevation: `1dp`
  - Background: `#FFFFFF` (Surface) or `#F5F5F5` (Surface Variant) - alternate
  - Padding: `16px` all sides
  - Left border accent: `4px` solid (philosopher color)
  - Border radius: `12px` (with left border extending to edge)

**Content Structure:**

**Header Row** (horizontal layout):

- **Philosopher Avatar/Emoji**: `40px` × `40px`
  - Border radius: `20px` (circle)
  - Spacing: `12px` right

- **Philosopher Name**:
  - Typography: `titleMedium` (16px/24px)
  - Color: `#1A1A1A` (On Surface)
  - Spacing: `8px` right

- **Tradition Chip**:
  - Component: M3 AssistChip (small)
  - Typography: `labelMedium` (12px/16px)
  - Background: Philosopher color at 20% opacity
  - Text color: Philosopher color
  - Height: `24px`
  - Spacing: `8px` right

- **Timestamp**:
  - Typography: `labelSmall` (11px/16px)
  - Color: `#6B7280` (On Surface Variant)
  - Format: "MM:SS" or "X minutes ago"
  - Alignment: Right (flexible)

**Spacing**: `16px` below header row

**Argument Text**:

- Typography: `bodyLarge` (16px/24px)
- Color: `#1A1A1A` (On Surface)
- Line height: `24px`
- Max width: Full width
- Word wrap: Enabled

**Streaming Indicator** (when active):

- Component: Animated dots (`...`)
- Typography: `bodyLarge` (16px/24px)
- Color: `#6B7280` (On Surface Variant)
- Animation: 3 dots, sequential fade (1s cycle)

#### 4. Thinking Indicator

**Component**: M3 Card (subtle)

**Specifications:**

- **Card**:
  - Border radius: `12px`
  - Elevation: `0dp`
  - Background: `#E5E5E5` (Surface Container)
  - Padding: `16px`
  - Border: `1px` solid `#E5E5E5`

**Content**:

- **Text**: "{Philosopher Name} is thinking..."
  - Typography: `bodyMedium` (14px/20px), italic
  - Color: `#6B7280` (On Surface Variant)

- **Progress Indicator**:
  - Component: `CircularProgressIndicator`
  - Size: `20px` × `20px`
  - Color: `#1E3A5F` (Primary)
  - Spacing: `12px` left of text

**Layout**: Horizontal (indicator + text)

#### 5. Empty State

**Specifications:**

- **Container**: Centered, full width
- **Padding**: `48px` vertical

**Content**:

- **Message**: "Debate starting..."
  - Typography: `bodyLarge` (16px/24px)
  - Color: `#6B7280` (On Surface Variant)
  - Alignment: Center

- **Loading Indicator**:
  - Component: `CircularProgressIndicator`
  - Size: `40px` × `40px`
  - Color: `#1E3A5F` (Primary)
  - Spacing: `16px` above message

### Visual Distinction

- **Philosopher Colors**: Each philosopher has distinct left border color
- **Card Alternation**: Alternate between Surface and Surface Variant backgrounds
- **Typography Hierarchy**: Clear distinction between philosopher name, tradition, and argument text
- **Spacing**: Consistent `16px` spacing maintains visual rhythm

---

## Screen 3: Philosopher Selection Screen

### Philosopher Selection Layout Structure

- **Container**: Scrollable grid
- **Background**: `#FAFAFA` (Background)
- **Padding**: `16px` on all sides
- **Sticky action bar**: Fixed at bottom

### Philosopher Selection Component Breakdown

#### 1. Screen Header

**Specifications:**

- **Title**: "Choose Philosophers"
  - Typography: `displaySmall` (36px/44px)
  - Color: `#1A1A1A` (On Surface)
  - Alignment: Left
  - Spacing: `8px` below

- **Subtitle**: "Select 2 philosophers for the debate"
  - Typography: `bodyMedium` (14px/20px)
  - Color: `#6B7280` (On Surface Variant)
  - Alignment: Left
  - Spacing: `24px` below

#### 2. Philosopher Grid

**Component**: M3 GridView

**Specifications:**

- **Cross-axis count**: 2 (mobile), 3 (tablet), 4 (desktop)
- **Main axis spacing**: `16px`
- **Cross axis spacing**: `16px`
- **Child aspect ratio**: `0.75` (width:height)
- **Padding**: `0px` (handled by container)

#### 3. Philosopher Card

**Component**: M3 Card (clickable)

**Specifications:**

- **Card** (default state):
  - Border radius: `12px`
  - Elevation: `1dp`
  - Background: `#FFFFFF` (Surface)
  - Border: `2px` solid transparent
  - Padding: `16px`
  - Cursor: Pointer (hover effect)

- **Card** (selected state):
  - Elevation: `4dp`
  - Border: `2px` solid `#1E3A5F` (Primary)
  - Background: `#F5F5F5` (Surface Variant)

**Content** (vertical stack, centered):

- **Avatar/Emoji**: `64px` × `64px`
  - Border radius: `32px` (circle)
  - Spacing: `12px` below

- **Name**:
  - Typography: `titleMedium` (16px/24px)
  - Color: `#1A1A1A` (On Surface)
  - Alignment: Center
  - Spacing: `8px` below

- **Tradition**:
  - Component: M3 AssistChip
  - Typography: `labelLarge` (14px/20px)
  - Background: Philosopher color at 20% opacity
  - Text color: Philosopher color
  - Height: `28px`
  - Alignment: Center
  - Spacing: `8px` below

- **Description**:
  - Typography: `bodySmall` (12px/16px)
  - Color: `#6B7280` (On Surface Variant)
  - Alignment: Center
  - Max lines: 2-3
  - Line height: `16px`
  - Spacing: `8px` below

- **Selection Indicator** (when selected):
  - Component: Checkmark icon
  - Size: `32px` × `32px`
  - Color: `#1E3A5F` (Primary)
  - Position: Top-right corner, `8px` offset
  - Background: `#FFFFFF` circle, `24px` diameter

**Spacing**: `8px` between all content elements

#### 4. Action Bar (Sticky Bottom)

**Component**: M3 Surface with high elevation

**Specifications:**

- **Container**:
  - Background: `#FFFFFF` (Surface)
  - Elevation: `8dp`
  - Padding: `16px` all sides
  - Border top: `1px` solid `#E5E5E5`
  - Min height: `72px`

**Content** (horizontal layout):

- **Selection Count**:
  - Typography: `bodyMedium` (14px/20px)
  - Color: `#6B7280` (On Surface Variant)
  - Text: "{X} selected" (dynamic)
  - Spacing: `16px` right

- **Start Debate Button**:
  - Component: M3 FilledButton
  - Text: "Start Debate"
  - Typography: `labelLarge` (14px/20px)
  - Color: `#FFFFFF` (On Primary)
  - Background: `#1E3A5F` (Primary)
  - Background (disabled): `#E5E5E5` (Surface Container)
  - Width: Flexible (fills remaining space)
  - Height: `40px`
  - Border radius: `20px`
  - Disabled when < 2 selected

### Philosopher Selection State Variations

#### Philosopher Selection Default State

- All cards in unselected state
- Action bar shows "0 selected"
- Button disabled

#### Philosopher Selection Active State

- Selected cards show border and elevation
- Selection count updates dynamically
- Button enabled when 2 selected

#### Philosopher Selection Maximum State

- Additional selections disabled (visual feedback)
- Action bar shows "2 selected"
- Button enabled

---

## Responsive Breakpoints

### Mobile

- **Width**: `375px` - `767px`
- **Philosopher Selection**: 2 columns (Question Screen), 2 columns (Selection Screen)
- **Content width**: Full width with `16px` padding
- **Typography**: Standard sizes

### Tablet

- **Width**: `768px` - `1023px`
- **Philosopher Selection**: 3 columns (Question Screen), 3 columns (Selection Screen)
- **Content width**: Max `600px` centered
- **Typography**: Standard sizes

### Desktop

- **Width**: `1024px`+
- **Philosopher Selection**: 4 columns (Question Screen), 4 columns (Selection Screen)
- **Content width**: Max `600px` centered
- **Typography**: Standard sizes

---

## Accessibility Requirements

### WCAG 2.1 AA Compliance

- **Color Contrast**:
  - Text on Surface: 4.5:1 minimum
  - Text on Primary: 4.5:1 minimum
  - Interactive elements: 3:1 minimum

- **Touch Targets**:
  - Minimum `44px` × `44px` for interactive elements
  - Spacing between targets: `8px` minimum

- **Focus Indicators**:
  - Visible focus rings on all interactive elements
  - Focus ring: `2px` solid `#1E3A5F` (Primary)
  - Border radius: Matches element

- **Screen Reader Support**:
  - Semantic labels for all interactive elements
  - Descriptive text for philosopher cards
  - Status announcements for debate updates

---

## Animation & Transitions

### Micro-interactions

- **Button Press**: Elevation change (1dp → 0dp), 100ms
- **Card Selection**: Elevation change (1dp → 4dp), 200ms ease-out
- **Text Streaming**: Character-by-character reveal, smooth
- **Loading Indicators**: Continuous rotation, 1s cycle
- **Scroll**: Smooth scrolling to latest argument

### State Transitions

- **Form Validation**: Error text fade-in, 200ms
- **Card Hover**: Subtle elevation increase, 150ms
- **Selection**: Border and elevation change, 200ms

---

## Notes for Implementation

1. **Figma Setup**: Use logical pixels (dp) for all measurements
2. **Component Library**: Create reusable components for cards, buttons, text fields
3. **Auto-layout**: Use Figma auto-layout for responsive components
4. **Variants**: Create component variants for states (default, selected, disabled, loading)
5. **Frames**: Create frames for mobile (375×812), tablet (768×1024), desktop (1440×900)
6. **Color Styles**: Define color styles matching the palette above
7. **Text Styles**: Define text styles matching the typography scale
8. **Spacing**: Use consistent spacing tokens throughout

---

## Design Principles Applied

1. **Clarity**: Uncluttered interface with clear visual hierarchy
2. **Distinction**: Each philosopher visually distinct through color and styling
3. **Minimalism**: Ample whitespace, focus on content
4. **Accessibility**: WCAG 2.1 AA compliant contrast and touch targets
5. **Responsiveness**: Adapts gracefully across device sizes
6. **Philosophical Aesthetic**: Classical color palette, thoughtful typography, elegant spacing

# Flutter Material Design 3 Component Mapping

This document maps wireframe elements to Flutter Material Design 3 (M3) components, providing implementation guidance for developers.

---

## Overview

Each wireframe element corresponds to specific Flutter widgets and M3 components. This mapping ensures consistency between design and implementation.

---

## Screen 1: Question Submission Screen

### App Header

**Wireframe Element**: Title "Agora" and subtitle

**Flutter Implementation**:

```dart
Column(
  mainAxisAlignment: MainAxisAlignment.center,
  children: [
    Text(
      'Agora',
      style: Theme.of(context).textTheme.displayLarge,
    ),
    SizedBox(height: 8),
    Text(
      'Pose a question. Witness the debate.',
      style: Theme.of(context).textTheme.bodyMedium?.copyWith(
        color: Theme.of(context).colorScheme.onSurfaceVariant,
      ),
    ),
  ],
)
```

**M3 Components**:

- `TextTheme.displayLarge` for title
- `TextTheme.bodyMedium` for subtitle
- `ColorScheme.onSurfaceVariant` for subtitle color

---

### Question Input Field

**Wireframe Element**: Multi-line text input with label and helper text

**Flutter Implementation**:

```dart
TextField(
  maxLines: 3,
  minLines: 3,
  maxLength: 500,
  decoration: InputDecoration(
    labelText: 'Your Question',
    helperText: '10-500 characters',
    counterText: '', // Custom counter below
    border: OutlineInputBorder(
      borderRadius: BorderRadius.circular(4),
    ),
    filled: false,
  ),
  style: Theme.of(context).textTheme.bodyLarge,
)
```

**M3 Components**:

- `TextField` widget
- `InputDecoration` with `OutlineInputBorder`
- `TextTheme.bodyLarge` for input text
- `TextTheme.bodyMedium` for label
- `TextTheme.bodySmall` for helper text

**Character Counter**:

```dart
Row(
  mainAxisAlignment: MainAxisAlignment.end,
  children: [
    Text(
      '${_questionController.text.length} / 500',
      style: Theme.of(context).textTheme.bodySmall?.copyWith(
        color: _isValid 
          ? Theme.of(context).colorScheme.onSurfaceVariant
          : Theme.of(context).colorScheme.error,
      ),
    ),
  ],
)
```

---

### Philosopher Selection Section

**Wireframe Element**: Horizontal scrollable list or grid of philosopher cards

**Flutter Implementation (Mobile - Horizontal Scroll)**:

```dart
SingleChildScrollView(
  scrollDirection: Axis.horizontal,
  child: Row(
    children: philosophers.map((philosopher) {
      return Padding(
        padding: EdgeInsets.only(right: 16),
        child: _PhilosopherSelectionCard(
          philosopher: philosopher,
          isSelected: selectedPhilosophers.contains(philosopher.id),
          onTap: () => _togglePhilosopher(philosopher.id),
        ),
      );
    }).toList(),
  ),
)
```

**Flutter Implementation (Desktop - Grid)**:

```dart
GridView.builder(
  gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
    crossAxisCount: 4,
    crossAxisSpacing: 16,
    mainAxisSpacing: 16,
  ),
  itemCount: philosophers.length,
  itemBuilder: (context, index) {
    return _PhilosopherSelectionCard(
      philosopher: philosophers[index],
      isSelected: selectedPhilosophers.contains(philosophers[index].id),
      onTap: () => _togglePhilosopher(philosophers[index].id),
    );
  },
)
```

**Philosopher Selection Card Component**:

```dart
class _PhilosopherSelectionCard extends StatelessWidget {
  final Philosopher philosopher;
  final bool isSelected;
  final VoidCallback onTap;

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: onTap,
      child: Card(
        elevation: isSelected ? 4 : 1,
        shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.circular(12),
          side: BorderSide(
            color: isSelected 
              ? Theme.of(context).colorScheme.primary
              : Colors.transparent,
            width: 2,
          ),
        ),
        child: Stack(
          children: [
            Container(
              width: 140,
              padding: EdgeInsets.all(16),
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Text(
                    philosopher.avatar,
                    style: TextStyle(fontSize: 48),
                  ),
                  SizedBox(height: 8),
                  Text(
                    philosopher.name,
                    style: Theme.of(context).textTheme.bodyLarge,
                    textAlign: TextAlign.center,
                  ),
                  SizedBox(height: 8),
                  Chip(
                    label: Text(
                      philosopher.tradition,
                      style: Theme.of(context).textTheme.labelMedium,
                    ),
                    backgroundColor: _getPhilosopherColor(philosopher.color)
                      .withOpacity(0.2),
                    labelStyle: TextStyle(
                      color: _getPhilosopherColor(philosopher.color),
                    ),
                  ),
                ],
              ),
            ),
            if (isSelected)
              Positioned(
                top: 8,
                right: 8,
                child: Icon(
                  Icons.check_circle,
                  color: Theme.of(context).colorScheme.primary,
                  size: 24,
                ),
              ),
          ],
        ),
      ),
    );
  }
}
```

**M3 Components**:

- `Card` widget with elevation
- `Chip` widget for tradition badge
- `RoundedRectangleBorder` for card shape
- `TextTheme.bodyLarge` for name
- `TextTheme.labelMedium` for chip text

---

### Submit Button

**Wireframe Element**: Primary action button

**Flutter Implementation**:

```dart
FilledButton(
  onPressed: _isFormValid ? _submitQuestion : null,
  style: FilledButton.styleFrom(
    minimumSize: Size(double.infinity, 40),
    shape: RoundedRectangleBorder(
      borderRadius: BorderRadius.circular(20),
    ),
    padding: EdgeInsets.symmetric(horizontal: 24),
  ),
  child: _isLoading
    ? SizedBox(
        width: 20,
        height: 20,
        child: CircularProgressIndicator(
          strokeWidth: 2,
          valueColor: AlwaysStoppedAnimation<Color>(
            Theme.of(context).colorScheme.onPrimary,
          ),
        ),
      )
    : Text(
        'Start Debate',
        style: Theme.of(context).textTheme.labelLarge,
      ),
)
```

**M3 Components**:

- `FilledButton` widget
- `FilledButton.styleFrom` for styling
- `CircularProgressIndicator` for loading state
- `TextTheme.labelLarge` for button text

---

## Screen 2: Debate Viewing Interface

### Sticky Header

**Wireframe Element**: Fixed header with question and "New Question" button

**Flutter Implementation**:

```dart
SliverAppBar(
  pinned: true,
  elevation: 2,
  backgroundColor: Theme.of(context).colorScheme.surface,
  flexibleSpace: Padding(
    padding: EdgeInsets.all(16),
    child: Row(
      crossAxisAlignment: CrossAxisAlignment.center,
      children: [
        Expanded(
          child: Text(
            question,
            style: Theme.of(context).textTheme.titleLarge,
            maxLines: 2,
            overflow: TextOverflow.ellipsis,
          ),
        ),
        TextButton(
          onPressed: _startNewQuestion,
          child: Text('New Question'),
        ),
      ],
    ),
  ),
)
```

**M3 Components**:

- `SliverAppBar` for sticky header
- `TextTheme.titleLarge` for question text
- `TextButton` for "New Question" action

---

### Debate Timeline

**Wireframe Element**: Scrollable list of argument cards

**Flutter Implementation**:

```dart
CustomScrollView(
  slivers: [
    // Sticky header (see above)
    SliverList(
      delegate: SliverBuilderDelegate(
        (context, index) {
          return Padding(
            padding: EdgeInsets.symmetric(
              horizontal: 16,
              vertical: 8,
            ),
            child: _ArgumentCard(
              argument: arguments[index],
            ),
          );
        },
        childCount: arguments.length,
      ),
    ),
    // Thinking indicator if active
    if (isThinking)
      SliverToBoxAdapter(
        child: _ThinkingIndicator(philosopher: currentPhilosopher),
      ),
  ],
)
```

**M3 Components**:

- `CustomScrollView` with `SliverList`
- `SliverAppBar` for sticky header
- Auto-scroll to latest argument using `ScrollController`

---

### Argument Card

**Wireframe Element**: Card with philosopher info and argument text

**Flutter Implementation**:

```dart
class _ArgumentCard extends StatelessWidget {
  final Argument argument;

  @override
  Widget build(BuildContext context) {
    final philosopherColor = _getPhilosopherColor(argument.philosopherColor);
    
    return Card(
      elevation: 1,
      shape: RoundedRectangleBorder(
        borderRadius: BorderRadius.circular(12),
      ),
      child: Container(
        decoration: BoxDecoration(
          border: Border(
            left: BorderSide(
              color: philosopherColor,
              width: 4,
            ),
          ),
          borderRadius: BorderRadius.circular(12),
        ),
        padding: EdgeInsets.all(16),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            // Header row
            Row(
              children: [
                CircleAvatar(
                  radius: 20,
                  child: Text(argument.philosopherAvatar),
                ),
                SizedBox(width: 12),
                Text(
                  argument.philosopherName,
                  style: Theme.of(context).textTheme.titleMedium,
                ),
                SizedBox(width: 8),
                Chip(
                  label: Text(
                    argument.tradition,
                    style: Theme.of(context).textTheme.labelMedium,
                  ),
                  backgroundColor: philosopherColor.withOpacity(0.2),
                  labelStyle: TextStyle(color: philosopherColor),
                ),
                Spacer(),
                Text(
                  _formatTimestamp(argument.timestamp),
                  style: Theme.of(context).textTheme.labelSmall?.copyWith(
                    color: Theme.of(context).colorScheme.onSurfaceVariant,
                  ),
                ),
              ],
            ),
            SizedBox(height: 16),
            // Argument text
            Text(
              argument.content,
              style: Theme.of(context).textTheme.bodyLarge,
            ),
            // Streaming indicator if active
            if (argument.isStreaming)
              Padding(
                padding: EdgeInsets.only(top: 8),
                child: Text(
                  '...',
                  style: Theme.of(context).textTheme.bodyLarge?.copyWith(
                    color: Theme.of(context).colorScheme.onSurfaceVariant,
                  ),
                ),
              ),
          ],
        ),
      ),
    );
  }
}
```

**M3 Components**:

- `Card` widget
- `RoundedRectangleBorder` for card shape
- `CircleAvatar` for philosopher avatar
- `Chip` for tradition badge
- `TextTheme.titleMedium` for philosopher name
- `TextTheme.bodyLarge` for argument text
- `TextTheme.labelSmall` for timestamp

**Streaming Text Animation with Serverpod**:

```dart
class StreamingText extends StatefulWidget {
  final Stream<Argument> argumentStream;
  final int argumentId;

  @override
  _StreamingTextState createState() => _StreamingTextState();
}

class _StreamingTextState extends State<StreamingText> {
  String _currentText = '';
  bool _isStreaming = false;

  @override
  void initState() {
    super.initState();
    _listenToStream();
  }

  void _listenToStream() {
    widget.argumentStream.listen(
      (argument) {
        if (argument.id == widget.argumentId) {
          setState(() {
            _currentText = argument.content;
            _isStreaming = argument.isStreaming ?? false;
          });
        }
      },
      onError: (error) {
        // Handle streaming errors
        setState(() {
          _isStreaming = false;
        });
      },
    );
  }

  @override
  Widget build(BuildContext context) {
    return Text(
      _currentText + (_isStreaming ? '...' : ''),
      style: Theme.of(context).textTheme.bodyLarge,
    );
  }
}
```

**Serverpod Streaming Client Usage**:

```dart
// In your debate service or state management
Stream<Argument> streamDebate(int debateId) {
  return client.debate.streamDebate(debateId);
}

// Usage in widget
StreamBuilder<Argument>(
  stream: debateService.streamDebate(debateId),
  builder: (context, snapshot) {
    if (snapshot.hasData) {
      return StreamingText(
        argumentStream: debateService.streamDebate(debateId),
        argumentId: snapshot.data!.id!,
      );
    }
    return CircularProgressIndicator();
  },
)
```

---

### Thinking Indicator

**Wireframe Element**: Card showing "Philosopher is thinking..."

**Flutter Implementation**:

```dart
class _ThinkingIndicator extends StatelessWidget {
  final Philosopher philosopher;

  @override
  Widget build(BuildContext context) {
    return Card(
      elevation: 0,
      color: Theme.of(context).colorScheme.surfaceContainerHighest,
      shape: RoundedRectangleBorder(
        borderRadius: BorderRadius.circular(12),
      ),
      child: Padding(
        padding: EdgeInsets.all(16),
        child: Row(
          children: [
            SizedBox(
              width: 20,
              height: 20,
              child: CircularProgressIndicator(
                strokeWidth: 2,
                valueColor: AlwaysStoppedAnimation<Color>(
                  Theme.of(context).colorScheme.primary,
                ),
              ),
            ),
            SizedBox(width: 12),
            Text(
              '${philosopher.name} is thinking...',
              style: Theme.of(context).textTheme.bodyMedium?.copyWith(
                fontStyle: FontStyle.italic,
                color: Theme.of(context).colorScheme.onSurfaceVariant,
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

**M3 Components**:

- `Card` widget with `elevation: 0`
- `ColorScheme.surfaceContainerHighest` for background
- `CircularProgressIndicator` for loading animation
- `TextTheme.bodyMedium` with italic style

---

**Note:** Philosopher selection is integrated into the Question Submission Screen. A separate philosopher selection screen is not part of the MVP.

---

## Color System Implementation

### Theme Configuration

**Flutter Implementation**:

```dart
ThemeData(
  useMaterial3: true,
  colorScheme: ColorScheme.fromSeed(
    seedColor: Color(0xFF1E3A5F),
    brightness: Brightness.light,
  ).copyWith(
    primary: Color(0xFF1E3A5F),
    primaryContainer: Color(0xFF2D4A6F),
    secondary: Color(0xFF6B7280),
    secondaryContainer: Color(0xFF9CA3AF),
    surface: Color(0xFFFFFFFF),
    surfaceVariant: Color(0xFFF5F5F5),
    surfaceContainerHighest: Color(0xFFE5E5E5),
    background: Color(0xFFFAFAFA),
    error: Color(0xFFDC2626),
    onPrimary: Color(0xFFFFFFFF),
    onSecondary: Color(0xFFFFFFFF),
    onSurface: Color(0xFF1A1A1A),
    onSurfaceVariant: Color(0xFF6B7280),
    onError: Color(0xFFFFFFFF),
  ),
  textTheme: TextTheme(
    displayLarge: TextStyle(
      fontSize: 57,
      height: 64 / 57,
      fontWeight: FontWeight.w400,
    ),
    displaySmall: TextStyle(
      fontSize: 36,
      height: 44 / 36,
      fontWeight: FontWeight.w400,
    ),
    titleLarge: TextStyle(
      fontSize: 22,
      height: 28 / 22,
      fontWeight: FontWeight.w500,
    ),
    titleMedium: TextStyle(
      fontSize: 16,
      height: 24 / 16,
      fontWeight: FontWeight.w500,
    ),
    bodyLarge: TextStyle(
      fontSize: 16,
      height: 24 / 16,
      fontWeight: FontWeight.w400,
    ),
    bodyMedium: TextStyle(
      fontSize: 14,
      height: 20 / 14,
      fontWeight: FontWeight.w400,
    ),
    bodySmall: TextStyle(
      fontSize: 12,
      height: 16 / 12,
      fontWeight: FontWeight.w400,
    ),
    labelLarge: TextStyle(
      fontSize: 14,
      height: 20 / 14,
      fontWeight: FontWeight.w500,
    ),
    labelMedium: TextStyle(
      fontSize: 12,
      height: 16 / 12,
      fontWeight: FontWeight.w500,
    ),
    labelSmall: TextStyle(
      fontSize: 11,
      height: 16 / 11,
      fontWeight: FontWeight.w500,
    ),
  ),
)
```

---

## Spacing Utilities

### Spacing Constants

**Flutter Implementation**:

```dart
class AppSpacing {
  static const double space4 = 4.0;
  static const double space8 = 8.0;
  static const double space12 = 12.0;
  static const double space16 = 16.0;
  static const double space24 = 24.0;
  static const double space32 = 32.0;
  static const double space40 = 40.0;
  static const double space48 = 48.0;
}
```

**Usage**:

```dart
SizedBox(height: AppSpacing.space16)
Padding(padding: EdgeInsets.all(AppSpacing.space24))
```

---

## Helper Functions

### Philosopher Color Mapping

```dart
Color _getPhilosopherColor(String colorName) {
  final colorMap = {
    'blue': Color(0xFF3B82F6),
    'purple': Color(0xFF8B5CF6),
    'pink': Color(0xFFEC4899),
    'green': Color(0xFF10B981),
    'orange': Color(0xFFF59E0B),
    'teal': Color(0xFF14B8A6),
    'indigo': Color(0xFF6366F1),
  };
  return colorMap[colorName.toLowerCase()] ?? Color(0xFF6B7280);
}
```

### Timestamp Formatting

```dart
String _formatTimestamp(DateTime timestamp) {
  final now = DateTime.now();
  final difference = now.difference(timestamp);
  
  if (difference.inMinutes < 1) {
    return 'Just now';
  } else if (difference.inMinutes < 60) {
    return '${difference.inMinutes}m ago';
  } else {
    return '${difference.inHours}h ago';
  }
}
```

---

## State Management Notes

### Form Validation

```dart
bool get _isFormValid {
  return _questionController.text.length >= 10 &&
         _questionController.text.length <= 500 &&
         selectedPhilosophers.length == 2;
}
```

### Loading States

```dart
bool _isLoading = false;

Future<void> _submitQuestion() async {
  setState(() => _isLoading = true);
  try {
    await debateService.startDebate(
      question: _questionController.text,
      philosopherIds: selectedPhilosophers,
    );
  } finally {
    setState(() => _isLoading = false);
  }
}
```

---

## Accessibility Considerations

### Semantic Labels

```dart
Semantics(
  label: 'Question input field',
  hint: 'Enter your philosophical question, 10-500 characters',
  child: TextField(...),
)
```

### Touch Targets

Ensure all interactive elements meet minimum `44px × 44px` touch target size:

```dart
Material(
  color: Colors.transparent,
  child: InkWell(
    onTap: onTap,
    child: Container(
      constraints: BoxConstraints(
        minWidth: 44,
        minHeight: 44,
      ),
      child: content,
    ),
  ),
)
```

---

## Performance Optimization

### List Optimization

Use `ListView.builder` or `GridView.builder` for large lists:

```dart
ListView.builder(
  itemCount: arguments.length,
  itemBuilder: (context, index) {
    return _ArgumentCard(argument: arguments[index]);
  },
)
```

### Image Optimization

For philosopher avatars (if using images instead of emojis):

```dart
CachedNetworkImage(
  imageUrl: philosopher.avatarUrl,
  placeholder: (context, url) => CircularProgressIndicator(),
  errorWidget: (context, url, error) => Icon(Icons.error),
)
```

---

## Testing Considerations

### Widget Tests

Test each component with different states:

```dart
testWidgets('PhilosopherCard shows selected state', (tester) async {
  await tester.pumpWidget(
    MaterialApp(
      home: _PhilosopherCard(
        philosopher: testPhilosopher,
        isSelected: true,
        onTap: () {},
      ),
    ),
  );
  
  expect(find.byIcon(Icons.check_circle), findsOneWidget);
});
```

---

## Additional Resources

- [Flutter Material Design 3](https://docs.flutter.dev/ui/design/material)
- [Material Design 3 Guidelines](https://m3.material.io/)
- [Flutter Widget Catalog](https://docs.flutter.dev/ui/widgets)
- [Flutter Accessibility](https://docs.flutter.dev/ui/accessibility)

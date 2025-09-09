# SuperButton

An advanced button component for Budibase applications with multiple action modes, styling options, and interaction capabilities including timers, loops, and conditional execution.

## 🚀 Features

### Action Modes

- **Normal Mode**: Standard click-to-action functionality
- **Timer Mode**: Scheduled auto-execution at configurable intervals
- **Loop Mode**: Batch processing of arrays or CSV data
- **Conditional Mode**: If/else logic for dynamic action execution

### Visual Customization

- **Multiple Styles**: Primary, Secondary, Warning, Action, Over Background, and Flat White variants
- **Size Options**: Extra Small (XS), Small (S), Medium (M), Large (L)
- **Icon Support**: Configurable icons before/after text or icon-only buttons
- **Quiet Mode**: Minimal styling for subtle interactions

### Advanced Execution

- **Batch Processing**: Loop through arrays or CSV data with customizable delays
- **Conditional Logic**: Dynamic action execution based on expressions
- **Timer Automation**: Scheduled execution from 1 second intervals
- **Event Integration**: Full Budibase event system support

## 🎯 Usage Instructions

### Basic Setup

1. Add the SuperButton component to your screen
2. Configure the button text and basic styling
3. Select your action mode (Normal, Timer, Loop, or Conditional)
4. Set up the appropriate action flows

### Action Modes

#### Normal Mode

- **Standard button**: Click to trigger actions
- **Single execution**: Each click runs the configured actions
- **Event handling**: Standard Budibase event system integration

#### Timer Mode

- **Auto-execution**: Button runs actions automatically at set intervals
- **Configurable timing**: Set interval from 1 second to any desired duration
- **Background processing**: Continues running when users aren't interacting

#### Loop Mode

- **Batch processing**: Process arrays or CSV data one by one
- **Delay control**: Configurable pauses between iterations
- **Progress context**: Access current iteration index and value
- **Start/end events**: Actions that run before/after the entire loop

#### Conditional Mode

- **Dynamic execution**: Run different actions based on expressions
- **If/else logic**: Execute actions when condition is true or false
- **Expression-based**: Use JavaScript expressions for decision making

### Styling Configuration

#### Visual Options

- **Button Type**: Choose from Primary, Secondary, Warning, Action, etc.
- **Size**: Select XS, S, M, or L sizing
- **Quiet**: Enable for minimal/subtle button styling
- **Disabled**: Enable to disable button interaction

#### Icon Configuration

- **Icon selection**: Choose from available icon set
- **Icon placement**: Before text, after text, or icon-only
- **Icon-only mode**: Remove text for icon-only buttons

## 🔧 Configuration Properties

### Basic Settings

- **Text**: Button display text (default: "Action")
- **Button Class**: Button or Action Button variant
- **Type**: Visual style - Action, Primary, Secondary, Warning, Over Background, Flat White
- **Size**: XS, S, M, L sizing options

### Interaction Settings

- **Icon**: Optional icon selection
- **Icon After Text**: Place icon after (not before) text
- **Icon Only**: Display only icon, no text
- **Quiet**: Minimal styling mode
- **Disabled**: Disable button interaction

### Action Mode Settings

- **Actions Mode**: Normal, Timer, Loop, or Conditional
- **Timer Duration**: Auto-execution interval (timer mode)
- **Loop Source**: Array or CSV data (loop mode)
- **Loop Delay**: Pause between iterations (loop mode, default 750ms)
- **Condition**: Expression for evaluation (conditional mode)

## 📋 Action Mode Examples

### Normal Mode - Simple Action

Configure a standard button that saves data:

- Text: "Save Changes"
- Type: Primary
- Actions Mode: Normal
- On Click: Add action to save current form data

### Timer Mode - Auto-refresh

Configure a button that refreshes data every 30 seconds:

- Text: "Auto Refresh"
- Type: Secondary
- Actions Mode: Timer
- Timer Duration: 30 seconds
- On Timer: Refresh datasource actions

### Loop Mode - Batch Processing

Configure a button that processes a list of items:

- Text: "Process All"
- Type: Action
- Actions Mode: Loop
- Loop Source: `{{ selectedItems }}`
- Loop Delay: 1000ms (between items)
- Before Loop: Show loading indicator
- Loop Actions: Process individual item
- After Loop: Hide loading, show completion message

### Conditional Mode - Smart Action

Configure a button with different behaviors:

- Text: "Submit"
- Type: Primary
- Actions Mode: Conditional
- Condition: `{{ formData.valid }}`
- If True: Submit form, show success
- Else: Show validation errors, highlight issues

## 🎨 Styling Examples

### Primary Action Button

- Type: Primary
- Size: Large
- Icon: Checkmark (after text)
- Text: "Confirm Order"

### Secondary Navigation

- Type: Secondary
- Size: Medium
- Icon: ArrowRight
- Text: "Continue"
- Quiet: Enabled

### Warning Action

- Type: Warning
- Size: Small
- Text: "Delete Item"
- Icon: Trash (before text)

### Icon-Only Button

- Icon: ThreeDots
- Icon Only: Enabled
- Size: Small
- Type: Secondary

## 🔗 Integration

### Budibase Actions

- **Navigation**: Page routing and screen changing
- **Data Updates**: Create, update, delete operations
- **User Interactions**: Show notifications, confirmations, prompts
- **External APIs**: REST API calls and integrations

### Context Integration

- **Form Data**: Access current form values
- **Page State**: Use screen-level variables
- **User Information**: Current user context
- **Data Sources**: Selected items and current records

### Advanced Examples

#### Dynamic Button State

```js
// Button text based on form state
{
  {
    formData.saved ? "Update Changes" : "Save New";
  }
}

// Button type based on priority
{
  {
    task.priority === "high" ? "warning" : "primary";
  }
}
```

#### Conditional Visibility

```js
// Show button only for admins
{
  {
    currentUser.role === "admin";
  }
}

// Hide button when form is pristine
{
  {
    !formData.modified;
  }
}
```

## 📱 Responsiveness

- **Automatic sizing**: Adapts to container space
- **Touch-friendly**: Proper sizing for mobile devices
- **Flexible content**: Text and icon layout adjustments
- **Accessibility**: Screen reader support and keyboard navigation

## 🐛 Troubleshooting

### Common Issues

- **Actions not firing**: Check event configuration and component state
- **Timer not working**: Verify timer duration and component visibility
- **Loop hanging**: Check loop data source and delay settings
- **Conditional logic**: Validate JavaScript expressions syntax

### Performance Notes

- **Timer efficiency**: Consider interval length for resource usage
- **Loop delays**: Minimum 100ms delays prevent system overload
- **Conditional evaluation**: Complex expressions may impact performance
- **Batch operations**: Large loops may require pagination

Find out more about developing [Custom Plugins](https://docs.budibase.com/docs/custom-plugin) and [Budibase](https://github.com/Budibase/budibase).

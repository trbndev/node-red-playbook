# Color-Coding for Node Groups

A consistent color scheme helps developers quickly identify the purpose and function of different node groups. The following color-coding system should be applied to all flows:

## Standard Color Scheme

| Group Type | Color | Hex Code | Preview | Purpose |
|------------|-------|----------|---------|---------|
| **Main Flow** | Blue | `#1A75FF` | <span style="display:inline-block;width:20px;height:20px;background:#1A75FF;border:1px solid #000"></span> | Primary processing path and core business logic |
| **On Success** | Green | `#2CA02C` | <span style="display:inline-block;width:20px;height:20px;background:#2CA02C;border:1px solid #000"></span> | Success handlers, confirmations, and positive outcomes |
| **On Error** | Red | `#D62728` | <span style="display:inline-block;width:20px;height:20px;background:#D62728;border:1px solid #000"></span> | Error handling, fallbacks, and recovery procedures |
| **Utilities** | Purple | `#9467BD` | <span style="display:inline-block;width:20px;height:20px;background:#9467BD;border:1px solid #000"></span> | Helper functions, formatters, and utilities |
| **Data Transform** | Orange | `#FF7F0E` | <span style="display:inline-block;width:20px;height:20px;background:#FF7F0E;border:1px solid #000"></span> | Data manipulation, conversion, and restructuring |
| **Input/Triggers** | Teal | `#17BECF` | <span style="display:inline-block;width:20px;height:20px;background:#17BECF;border:1px solid #000"></span> | Flow entry points, triggers, and events |
| **External Systems** | Brown | `#8C564B` | <span style="display:inline-block;width:20px;height:20px;background:#8C564B;border:1px solid #000"></span> | API calls, database operations, external services |
| **Subflows** | Gray | `#7F7F7F` | <span style="display:inline-block;width:20px;height:20px;background:#7F7F7F;border:1px solid #000"></span> | Encapsulated reusable functionality |

## Color Palette Preview

<div style="display:flex;flex-wrap:wrap;gap:10px;margin:20px 0;">
  <div style="width:100px;height:80px;background:#1A75FF;color:white;display:flex;align-items:center;justify-content:center;border-radius:5px;">Main Flow</div>
  <div style="width:100px;height:80px;background:#2CA02C;color:white;display:flex;align-items:center;justify-content:center;border-radius:5px;">On Success</div>
  <div style="width:100px;height:80px;background:#D62728;color:white;display:flex;align-items:center;justify-content:center;border-radius:5px;">On Error</div>
  <div style="width:100px;height:80px;background:#9467BD;color:white;display:flex;align-items:center;justify-content:center;border-radius:5px;">Utilities</div>
  <div style="width:100px;height:80px;background:#FF7F0E;color:black;display:flex;align-items:center;justify-content:center;border-radius:5px;">Data Transform</div>
  <div style="width:100px;height:80px;background:#17BECF;color:black;display:flex;align-items:center;justify-content:center;border-radius:5px;">Input/Triggers</div>
  <div style="width:100px;height:80px;background:#8C564B;color:white;display:flex;align-items:center;justify-content:center;border-radius:5px;">External Systems</div>
  <div style="width:100px;height:80px;background:#7F7F7F;color:white;display:flex;align-items:center;justify-content:center;border-radius:5px;">Subflows</div>
</div>

## How to Apply Colors

1. Select the node group in Node-RED
2. Open the group properties panel
3. Select "Appearance" tab
4. Apply the appropriate background color using the color picker or hex code
5. Adjust text color for readability if needed

## Visual Organization Guidelines

- Position similar colored groups near each other when possible
- Use group borders to further distinguish between related groups
- Add group labels that complement the color-coding system
- Consider adding a small color key as a comment node in complex flows

## Accessibility Consideration

For teams with colorblind members, consider adding distinctive patterns or icons to groups in addition to colors, or use an alternative color palette designed for color vision deficiencies.

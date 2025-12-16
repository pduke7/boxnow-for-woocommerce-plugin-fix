# Box Now Delivery Plugin Fix
This repository contains fixes for the BOX NOW Delivery woocommerce plugin (https://wordpress.org/plugins/box-now-delivery/)

## Changes Made

### Max Weight Validation
- Enhanced the weight validation logic to properly check total cart weight against the configured limit
- The shipping method now correctly calculates total cart weight (including quantities) and hides the BOX NOW delivery option when exceeded
- Fixed validation to check dimensions separately from weight (previously could skip weight check if dimensions passed)
- Weight validation can be disabled by setting the limit to 0 or leaving it empty

### Enhanced Admin UI for Weight Configuration
- Added a dedicated "Weight Restrictions" section in the shipping method settings
- Changed field title from "Max Weight" to "Max Total Cart Weight" for clarity
- Improved field description with detailed instructions about:
  - What the weight limit applies to (total cart weight, not individual items)
  - Which unit to use (must match WooCommerce product settings)
  - How to disable the validation (set to 0 or empty)
  - Practical example (e.g., enter 20 for a 20kg limit)
- Changed placeholder text to be more descriptive: "e.g., 20 (for 20kg)"
- Improved step precision from 0.1 to 0.01 for more accurate weight entry

## Technical Details

### Files Modified
- `includes/box-now-delivery-shipping-method.php`
  - Updated `has_oversized_products()` method (lines 257-286) to properly calculate total cart weight
  - Enhanced form fields configuration (lines 135-151) with better UI labels and descriptions

### How It Works
The `has_oversized_products()` private method now:
1. Calculates the total cart weight by summing (product weight × quantity) for all items
2. Checks if any individual item exceeds dimension limits
3. Separately checks if total cart weight exceeds the configured limit
4. Returns true if either dimensions OR weight limits are exceeded, hiding the shipping method

## Attribution
Original plugin developed by BOXNOW

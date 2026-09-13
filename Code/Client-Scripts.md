# Client Scripts

Client Scripts are used to validate booking information and control field behavior on the booking form.

## Booking Date Validation

Used in the Booking table to validate the booking date entered by the user.

```javascript
function onChange(control, oldValue, newValue, isLoading) {

    if (isLoading || newValue == '') {
        return;
    }

    var selectedDate = new Date(newValue);
    var today = new Date();

    today.setHours(0, 0, 0, 0);

    if (selectedDate < today) {
        g_form.showFieldMsg(
            'booking_date',
            'Please select a current or future date.',
            'error'
        );

        g_form.setValue('booking_date', '');
    }
}
```

## Available Slot Selection

Used to filter the Selected Slot field based on the booking date and show only available slots for the selected date.

```javascript
function onChange(control, oldValue, newValue, isLoading) {

    if (isLoading) {
        return;
    }

    g_form.clearValue('selected_slot');

    if (newValue == '') {
        return;
    }

    var query = 'slot_date=' + newValue + '^availability=Available';

    g_form.setQuery('selected_slot', query);
}
```

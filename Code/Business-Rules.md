# Business Rules

Business Rules are used to control booking records and maintain slot availability.

## Prevent Duplicate Booking

This Business Rule runs before a booking is inserted or updated. It checks whether the selected slot already has an active booking.

```javascript
(function executeRule(current, previous) {

    if (current.selected_slot.nil() || current.status == 'Cancelled') {
        return;
    }

    var booking = new GlideRecord('x_sba_booking');
    booking.addQuery('selected_slot', current.selected_slot);
    booking.addQuery('status', '!=', 'Cancelled');

    if (!current.isNewRecord()) {
        booking.addQuery('sys_id', '!=', current.sys_id);
    }

    booking.query();

    if (booking.next()) {
        gs.addErrorMessage('The selected slot is already booked.');
        current.setAbortAction(true);
    }

})(current, previous);
```

## Update Slot Availability

This Business Rule updates the availability of the selected slot when a booking is confirmed or cancelled.

```javascript
(function executeRule(current, previous) {

    if (current.selected_slot.nil()) {
        return;
    }

    var slot = new GlideRecord('x_sba_slot');

    if (slot.get(current.selected_slot)) {

        if (current.status.changesTo('Confirmed')) {
            slot.availability = 'Booked';
            slot.update();
        }

        if (current.status.changesTo('Cancelled')) {
            slot.availability = 'Available';
            slot.update();
        }
    }

})(current, previous);
```

## Booking Status

The Booking table uses the following status values:

- Requested
- Confirmed
- Cancelled

The status is used to control the booking lifecycle and determine the availability of the selected slot.

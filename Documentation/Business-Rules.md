# Business Rules

Business Rules are used to control booking records and maintain slot availability.

## Duplicate Booking Prevention

A Business Rule checks whether the selected slot is already booked before allowing another booking for the same slot.

This prevents multiple users from booking the same available slot.

## Slot Availability Update

The slot availability is updated when a booking is confirmed.

The slot is changed from available to booked when the booking is confirmed.

When a booking is cancelled, the slot is made available again.

## Booking Status

The booking status is updated based on the action performed on the booking record.

This helps maintain the current state of each booking request.

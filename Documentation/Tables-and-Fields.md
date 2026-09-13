# Tables and Fields

The Slot Booking and Availability Management System uses two custom tables to manage slots and booking requests.

## Slot Table

The Slot table stores information about the available time slots.

The table contains fields such as:

- Slot Date
- Start Time
- End Time
- Availability

The Availability field is used to identify whether a slot is available or already booked.

## Booking Table

The Booking table stores the booking requests submitted by users.

The table contains fields such as:

- Requester
- Booking Date
- Selected Slot
- Purpose
- Status

The Selected Slot field is linked to the Slot table so that each booking is associated with a specific slot.

The Booking table is also used to track the current status of each booking, including booking and cancellation details.

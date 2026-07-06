# Notes

## Fix explained: PHP 0 booking bug (Task 2)

The `rental_days()` function was supposed to bill inclusively, meaning both the start and end day of a rental count toward the total. Instead, it used plain date subtraction, which is exclusive, so a same-day rental computed 0 days and every other rental was undercharged by one day. I fixed this by adding 1 to the subtraction, which matches the inclusive rule stated in the business rules and the same logic already used correctly in the frontend's dayCount() function.

## Double-booking failure example (Task 1)

The original code wrongly allowed booking the Canon DSLR Camera for Jan 5–12, 2026, even though it overlaps the existing Jan 10–15 booking. The fixed dates_overlap() function now correctly detects the overlap and blocks it with a 409 error.

## AI use

I used Claude to help me understand the existing codebase, walk through why each bug occurred, and reason through the correct fix for each one rather than asking for finished code upfront. For the billing bug specifically, I checked that the logic made sense using a real-world comparison: renting a book from a library, where the day you pick it up already counts as day one, which matched the inclusive billing rule stated in the business rules. I also ran the application locally and manually reproduced each bug before applying a fix, then re-tested the same scenario afterward to confirm it was resolved. I wrote the fixes myself based on that understanding rather than using AI-generated code directly.
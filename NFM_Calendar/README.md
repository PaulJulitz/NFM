# Yearly Calendar Planner

This calendar stores three kinds of user data:

1) Selected dates by category (Person A, Person B, Special day)
2) User-selected kindergarten closing days
3) User-selected events

All are stored in-memory in the `state` object inside `NFM_Calendar/index.html`.
You can save them to a JSON file in the `NFM_Calendar` folder using the Save button.

## Date key format

All stored dates use the same key format:

```
YYYY-MM-DD
```

Example: `2026-07-24`

## Where user selections are stored

### Category selections (holidays for people / special days)

Stored in:

```
state.selections
```

Structure:

```
{
  "2026-07-10": ["a", "b"],
  "2026-07-11": ["a"],
  "2026-08-05": ["b", "c"],
  "2026-09-02": ["c"]
}
```

Values map to the category ids defined in the `categories` array:

- `a` = Holiday - Person A
- `b` = Holiday - Person B
- `c` = Special day

When a user clicks a date while "Category selection" mode is active, the category is toggled inside `state.selections`.

### Kindergarten closing days (user-selected)

Stored in:

```
state.userClosingDays
```

Structure:

```
{
  "Berlin": {
    "2026-07-24": "User selected closing day"
  },
  "Hamburg": {
    "2026-08-07": "User selected closing day"
  }
}
```

When a user clicks a date while "Kindergarten closing days" mode is active, the date is added to or removed from `state.userClosingDays` for the active region.

### Events (user-selected)

Stored in:

```
state.events
```

Structure:

```
{
  "Berlin": {
    "2026-09-12": ["Summer party", "Family meetup"]
  }
}
```

When a user clicks a date while "Events" mode is active, the event name is added to or removed from `state.events` for the active region.

## How to prefill or edit stored data

Open `NFM_Calendar/index.html` and edit the data structures directly:

- Pre-fill holidays by people: update `state.selections`
- Pre-fill user closing days: update `state.userClosingDays`

You can also add official holidays and default closing days in:

- `holidayData`
- `closingDays`

These two are read-only inputs for the UI, while the user selections are stored in `state.selections`, `state.userClosingDays`, and `state.events`.

## Saving selections to a file

Click "Save selections" to export a JSON file containing:

```
{
  "year": 2026,
  "region": "Berlin",
  "selections": { ... },
  "userClosingDays": { ... },
  "events": { ... },
  "savedAt": "2026-01-20T09:15:00.000Z"
}
```

If your browser supports the File System Access API, you can choose the `NFM_Calendar` folder directly. Otherwise, the file is downloaded and you can move it into the `NFM_Calendar` folder manually.

## Loading selections from a file

Click "Load selections" and choose a previously saved JSON file. The calendar applies:

- `year` and `region`
- `selections`
- `userClosingDays`
- `events`

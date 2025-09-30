FET Timetable Viewer
====================

A small language selector is available: [English](README.md) · [العربية](README.ar.md)

A single-file HTML timetabling viewer for FET XML/.fet exports. Open `timetable_viewer.html` in a browser to view, explore and print timetables for Teachers, Students (groups & subgroups) and Rooms.

Quick start
-----------
1. Open the workspace folder and double-click `timetable_viewer.html` to open it in your browser.
   - You can open the file directly (file:///) or serve the folder and browse to it:

```bash
# Optional: serve the folder (recommended if you see CORS or local resource issues)
python -m http.server 8000
# Then open http://localhost:8000/timetable_viewer.html
```

2. Use the "Select FET XML Files" control to import one or more `.fet` / `.xml` files exported by FET.
3. Switch between the Teachers / Students / Rooms tabs and use the dropdowns to select an entity.
4. Use the Settings panel to adjust layout and color options. Use the Print options to generate printable reports.

Features
--------
- Parse and display FET timetable exports (teachers, students, rooms, activities).
- Vertical and horizontal timetable layouts.
- Print-friendly view with options to include Teachers, Students, Rooms (and a combined report).
- Accessibility: automatic contrast calculation for activity text (WCAG-based luminance) so labels remain readable.
- Automatic color-coding:
  - Students: activities colored consistently by Subject.
  - Teachers: activities colored consistently by Group/Class name.
  - Colors are generated deterministically so the same subject/group gets the same color every session.
- Handles groups and subgroups: student selection includes subgroup activities and teachers list aggregates subgroup teachers.

Settings & UI
-------------
- Table Layout: `vertical` (default) or `horizontal`.
- Base Color (for color generation): a base color is used to seed color generation. The app will generate distinct, readable colors per subject/group.
- RTL/LTR toggle for right-to-left languages.
- Reset Settings button restores defaults.

Printing
--------
- The Print panel generates a clean black/white or color-friendly print view depending on options.
- The students print view shows group name and subjects (no total hours) to keep pages concise.
- Teachers-by-subject for students is output as a 4-column table (Subject | Teacher | Subject | Teacher).

Customizing colors
------------------
If you want to change how colors are generated or the mapping rules, edit `timetable_viewer.html`:
- generateColorForKey(key) — deterministic color generation based on a key (subject or group name).
- getActivityBackgroundColor(activity, type) — chooses the key (subject for students, students/group for teachers).
- hslToHex(h, s, l) — converts generated HSL values to HEX.

Debugging tips
--------------
- Open the browser console (F12) to see debug logs. The app logs color assignments and other useful diagnostics.
- Common issues:
  - If nothing loads after importing files, check the browser console for parsing errors.
  - If activities show wrong colors, the console prints the key used for color generation (subject/group) and the computed hex color.
- After editing `timetable_viewer.html`, reload the page to pick up changes.

Development notes
-----------------
- This is a single-file app (no build step). All logic and styles are inside `timetable_viewer.html`.
- The code uses modern ES6 features; use a modern browser (Chrome, Firefox, Edge).
- If you want to host the viewer, serving via a static HTTP server (see Quick start) is recommended.

Contributing
------------
- Make a branch, edit files, and test locally. Keep changes small and well-scoped.
- If you add features, consider adding small unit tests or example files demonstrating the feature.

License
-------
- No license is included. Add a LICENSE file if you want to open-source this project.

Contact / Notes
---------------
- This viewer was customized to better handle FET group/subgroup logic, print formatting, RTL, and color accessibility.
- If you want additional features (export to CSV, improved color palettes, or theme options), I can add them.

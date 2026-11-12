# Changelog

## [0.34.1] – 2026-11-11
### Changed (owner's feedback: "vertical and horizontal look swapped")
- The drawing was right ("↓ Lodret" ran top to bottom), but the words read both ways – a "vertical
  gradient" can also mean a vertical split. The three choices are now small squares painted with the
  day's two colours, labelled "Hjørne til hjørne", "Top til bund" and "Venstre til højre".
- One rule for both: `GradientDir.weight()` is used by the widget blend and by the squares.
### Tests
- `GradientTest.directionsShowWhatTheySay`: on Neon (the owner's case) and Card, top-to-bottom
  changes only top↔bottom and left-to-right only left↔right; the weight rule's ends. Watched failing
  with the two directions swapped. A sheet of Neon in the three directions.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.34.0] – 2026-11-11
### Added (roadmap round 2)
- Look → Shape: corners (sharp / round / extra round) and "Visible background" 30–100 %.
  - Opacity in one place: the day is drawn with and without text and emoji; where the two agree
    it is the shape, which fades; where they differ it is text or emoji, which stays solid. Works
    with a gradient too.
  - Corners in one place (`widget/CornerScale.kt`): every rounded rectangle in the templates goes
    through `drawRound`/`addRound`, which scale the radius for the drawing in progress; effect
    outlines use the same scale, so the progress bar, snow and borders follow the new corners.
  - Kept in backups, in "My styles" and "apply to all"; presets reset them.
### Tests
- `ShapeTest`: opacity and corners reach every template, small and wide (circles, blobs and shapes
  already fully round are listed with the reason); the shape fades to half while the text stays
  solid, also with a gradient; sharp corners are filled, extra round are empty; the progress bar
  stays inside sharp and extra-round shapes; a sheet over a striped "wallpaper". Defaults
  pixel-identical to 0.27.0. Watched failing, one at a time: everything fading, outlines ignoring
  the corners (it named the Calendar), styles forgetting the opacity.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.33.0] – 2026-11-11
### Added (roadmap round 2)
- "My styles": "＋ Save as style" first in Look → Styles saves the day's whole look under a name
  (template, colour and gradient, second/third colour, phone colours, pattern, fonts, text colours
  and sizes, effect, animation, progress bar). Saved styles come first in the row with a preview;
  one tap applies one to the day; long-press renames or deletes. The day's own name, date, kind,
  emoji, photo, phone, time, reminder and "celebrated" always stay. Kept in backups; on import
  they join the phone's styles (same name: the phone's own wins).
- `data/Looks.kt`: the single list of what a "look" is; AGENTS.md says new look fields go there.
### Tests
- `StylesTest`: a reflection guard over every `Markday` field (look or the day's own – a new field
  fails with its name until placed); a styled day draws exactly like the original's look; rename,
  delete, replace; backup round trip and merge; the editor form applies and recognises a style.
  Watched failing, one at a time: `withLookOf` forgetting the gradient, backups dropping styles,
  an unplaced field. The editor dialogs themselves are not driven by a test (the form is).
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.32.0] – 2026-11-11
### Added (roadmap round 2)
- Colour gradient: "Gradient to" under the colour (Auto = one colour; My colours included), with
  diagonal / vertical / horizontal. Works in every template from one place: the day is drawn once
  in each colour and the two are blended across the shape, so everything in the day's colour gets
  the gradient and nothing else changes. Text is chosen against the middle of the gradient in both
  drawings, so it never fades between white and dark. The phone's colours (Material You) replace
  the gradient. Kept in backups; presets reset it; "apply to all" copies it.
### Tests
- `GradientTest`: every template changes, small and wide; both ends show in the chosen direction;
  the three directions differ; steady text on a light→dark gradient; sheets. One colour stays
  pixel-identical to 0.27.0 (52 references). `BackupTest` round trip and older backups. Watched
  failing, one at a time: second drawing in the first colour, direction ignored, gradient dropped
  from backups.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.31.0] – 2026-11-09
### Added (owner's request: "days" was very small)
- Text size per day in the editor (Text → Text size): name, number, unit ("dage") and date, 70–160 %
  in 5 % steps, with "Reset sizes". Multiplied with the phone's own tuning (Settings → widget
  tuning). Text only grows as far as the template has room. Kept in backups; presets reset them;
  "apply to all" copies them.
### Fixed
- Animated templates: when number and "dage" had to shrink together, the gap did not, so "dage"
  could be cut to "da…". The gap now shrinks with them.
- Ring (small): a bigger name grows its pill upwards instead of past the bottom edge.
### Tests
- `TextSizeTest`: every slider changes exactly the templates that show its text (small and wide);
  a bigger "dage" is bigger; at 160 % nothing is cut at the widget's edge (it caught the Ring pill);
  sizes multiply with tuning; sheets. Defaults pixel-identical to 0.27.0 (52 references).
  `BackupTest` round trip and older backups. Watched failing, one at a time: unit ignored by
  `roleScale`, sizes dropped from backups, animated templates ignoring the unit size.
### Published
- Uploaded to MarkdaysReleases on the owner's request (2026-11-09); public APK checked identical.

## [0.30.0] – 2026-11-09
### Added (owner's wish, roadmap 0.30–0.36 in docs/ROADMAP.md)
- "My colours": a colour made with the rainbow dialog is kept (newest first, at most 12, no
  duplicates) and shown first in every colour picker – colour, second and third colour, name and
  number colour – after a thin divider. Long-press asks to remove one. Kept in backups (merged on
  import).
### Tests
- `MyColorsTest`: order/limit/no duplicates/remove; backup round trip; a colour made once in the
  rainbow dialog shows in all five pickers. Watched failing, one at a time: dialog not saving,
  pickers not showing my colours, import dropping them.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.29.0] – 2026-11-08
### Added (owner's rule: three colours in every template)
- Rule written down in the new `AGENTS.md`: every template, small and wide, uses colour, second
  colour and third colour; kept by `AccentColourTest.everyTemplateUsesAllThreeColours`.
- Second colour where a template has no paper (19 templates did nothing with it): the text on
  Card, Bubble, Ticket, Minimal (name/date), Blob (small: the back blob, plus a third-colour edge on
  the front blob) and the animated cards; Glass: the panel; Neon: the background (kept dark);
  Photo: the shade (kept dark). White is automatic, so the look is unchanged until chosen.
### Changed
- Glass: the third colour is the rim and gloss (the panel moved to the second colour so a light
  second colour never becomes unreadable text on the light panel).
- Dark mode and the phone's colours leave the second colour alone where it is not paper
  (`Template.secondIsPaper`); an explicit text colour still wins over it.
- Editor hint for the second colour says what it does where there is no paper.
### Tests
- `everyTemplateUsesAllThreeColours`, `darkModeKeepsASecondColourThatIsText`, the Glass contrast
  check on the second colour, a sheet of the 19 templates with four second colours. Auto/white
  still pixel-identical to 0.27.0 (52 references). Watched failing, one at a time: Neon back to a
  fixed background, dark mode darkening every second colour.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.28.1] – 2026-11-08
### Added (owner's feedback on 0.28.0)
- The third colour is in every template, so the choice is always shown:
  - Calendar: an edge round the sheet; on the wide one the sticky note is the third colour (text
    follows its contrast).
  - Ring: an edge round the disc/card and the ring's track.
  - Clean, Arch (small): an edge round the shape; Arch (wide): the window.
  - Polaroid: a frame round the photo. Shapes: the big soft circle. Aura: the sheen.
- Auto keeps every template pixel-identical to 0.27.0.
### Tests
- `AccentColourTest.everyTemplateHasAThirdColour` (replaces the exact-set check): every template,
  small and wide, changes with a third colour. Watched failing with Clean's edge removed (it named
  Clean small and wide). Wide sheet of all templates (`docs/accent-wide.png`).
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.28.0] – 2026-11-08
### Added (owner's feedback on 0.27.1)
- "Third colour" (new `accentColor`, per day; Auto = white as before) paints the template's light
  parts on its own: Bubble's circle (filled solid when chosen) and gloss, the shine on Card and the
  animated cards, Glass's panel/gloss/rim/pattern, Minimal's and Photo's text, Ticket's perforation,
  Neon's core line, Blob's back layer. Shown in the editor only for those templates.
- Text on a filled third colour takes its own contrast (Bubble's number, Glass's text).
- Kept in backups; older backups without it get Auto. "Apply to all" and presets carry/reset it.
### Changed
- "Second colour" is the template's background/paper again, as before 0.27.1 (0.27.1 had tied the
  light parts to it, so in Bubble they could not differ from the background).
### Tests
- `AccentColourTest` (replaces `SecondColourTest`): the third colour changes exactly the templates
  the editor offers it for, small and wide; red Bubble with red paper still gets its own circle and
  paper does not move it; contrast of text on a light and a dark third colour; Auto pixel-identical
  to 0.27.0 (52 references). `BackupTest`: round trip and older backups.
- Watched failing on planted faults, one at a time: Bubble's circle on the second colour, the field
  dropped from backups, Glass text ignoring contrast.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.27.1] – 2026-11-08
### Changed (owner's feedback)
- "Paper" is renamed "Second colour" and is now the secondary colour of every template (same stored
  field, so saved days and backups are unchanged). Parts that were fixed white follow it: the shine
  on Card and the animated templates' cards, Bubble's inner circle and gloss, Glass's panel, gloss,
  rim and pattern, Minimal's text and line, Ticket's perforation, Neon's core line and texts, Blob's
  back layer. A chosen colour shows as a clear accent; white keeps the exact old look.
- Photo template: a light second colour colours the text; a dark one tints the shade under white
  text instead, so the text always reads.
- Editor: a short hint under "Second colour" says what it colours.
### Tests
- `SecondColourTest`: every template, small and wide, changes with a second colour other than white;
  with white, 52 pictures are pixel-identical to references drawn by the old code; a sheet of all
  templates in white and in blue (`docs/second-colour.png`). Watched failing with Bubble set back to
  fixed white (it named Bubble small and wide).
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.27.0] – 2026-11-08
### Added (owner's request)
- Filters on the main screen, from 5 mark days: chips "All (n)", "🎂 Birthdays (n)", "💞 Anniversaries",
  "🎉 Holidays", "✈️ Events" (only kinds you have), and 🔍 for a search on name or emoji (case does
  not matter). The chosen kind is remembered until changed; the counts follow the search. "No mark
  days match" with "Clear filter" when nothing is left.
### Tests
- `ListFilterTest`: all, by kind, by name/emoji ignoring case, both together, chip counts follow the
  search. Watched failing on planted faults (case-sensitive search, kind ignored, counts ignoring
  the search). Main-screen screenshot with the chips.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.26.3] – 2026-11-08
### Added (owner's feedback)
- Turn the photo with two fingers (twist), per widget size like the framing. Within 3° of straight
  (0/90/180/270°) it snaps to straight. Reset straightens it too. Where a turned photo does not
  reach the corners, the day's colour shows. The adjust view shows zoom and angle ("1,0× · 15°").
### Changed
- The − and + buttons are gone from the adjust view: the owner only used fingers and Reset.
### Tests
- `PhotoFrameTest`: snapping, a turned photo is drawn differently and only inside the shape, bare
  corners show the day's colour, small and wide turn on their own, older data carries the turn to
  the wide one, no turn in backups. Watched failing on planted faults (no snap, wide using the small
  turn, turn exported).
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.26.2] – 2026-11-08
### Changed (owner's feedback)
- The small and the wide widget now each have their own photo framing (zoom and shift), since one
  framing rarely suits both shapes. In the adjust view you drag and pinch on the widget you want to
  change; −/+ and Reset act on the one touched last, which is outlined, and a line says which one.
  Framings saved before start the wide widget from the small one's, so nothing jumps. Like the photo,
  neither framing is in a backup.
### Tests
- `PhotoFrameTest`: each size ignores the other's framing and follows its own, older saved framings
  carry over to the wide one, and no framing in backups. Watched failing on planted faults (wide
  using the small framing, old data starting from the centre, wide framing exported).
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.26.1] – 2026-11-08
### Changed (owner's feedback with screenshots)
- The photo could only move within its own overflow, so on the wide widget a face could not be moved
  far enough to the right, and it could not be zoomed out. Now it follows the finger also past the
  edge – its centre may go right up to the field's edge, so part of it always shows – and it zooms
  from ½× to 4×. Where the photo does not reach, the day's colour shows (a gradient), never smeared
  edge pixels: the photo is drawn once, clipped to the shape. Framings saved with 0.26.0 keep their
  values under the new meaning, so a photo adjusted there may need adjusting again.
### Tests
- `PhotoFrameTest` reworked: the photo's centre never leaves the field (any zoom/shift), centred at
  1× it still covers the field, shift ±½ puts the centre at the field's edge, ½× halves the scale,
  the chosen half shows, and the day's colour shows where the photo does not reach. Watched failing
  on planted faults (no shift limit, smeared edges, no zoom out).
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.26.0] – 2026-11-08
### Added
- Adjust the photo (Look → Photo → Adjust): a full-screen view with the small and the wide widget,
  large; drag to move the photo up, down and sideways, pinch to zoom (1–4×); −/+ and Reset as buttons.
  One framing for both sizes, shown together. The photo always covers its field: the focus only moves
  it within the overflow, so there is never an empty edge. A new photo starts centred at 1×.
  `docs/photo-framing.png`.
- Like the photo itself, the framing stays on the phone (not in backups).
### Tests
- `PhotoFrameTest`: the photo covers the field for every zoom and focus (also out-of-range values)
  in all four photo fields; focus −1/1 shows the photo's edges, zoom 2× doubles the scale, drag and
  pinch limits; the widget shows the chosen half of a red/blue photo; framing not in backups.
  Watched failing on planted faults (no clamping, focus ignored, framing exported).
### Not verified
- On the phones: how dragging and pinching feel. The adjust view is a dialog window that the test
  screenshots do not capture.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.25.1] – 2026-11-08
### Fixed
- Opening a day from a widget could trap you in the editor: the widget started a task holding only
  the editor, so X/back went to the home screen and the app icon or Recents brought the same editor
  back (only a force stop helped). Now every way in from outside – widget, list row, reminder,
  "Open" in the day menu – opens the list with the editor on top in a fresh task: X, back and Save
  return to the list, and the app opens normally afterwards.
### Tests
- `BackStackTest`: widget, list row, reminder and day menu all start [list, editor] in a fresh task
  with the right day. Watched failing with the old editor-only widget tap.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.25.0] – 2026-11-08
### Added
- Five new animated templates: Candle (flickering flame and breathing glow, for memorial days), Sun
  (pulsing rays, a drifting cloud), Easter egg (rocks and sways), Pumpkin (face glowing like a
  candle, bobbing), Graduation cap (the Danish "studenterhue": white crown, red band, black visor –
  tossed up, caught, settles). All with "how many times" variants. `docs/motif-frames.png`.
### Tests
- The existing motif audits cover the new pictures automatically, and caught real faults in the
  first drawings before they were fixed: the pumpkin's animations did not fit one loop (so "3 times"
  would have ended wrong), and Candle, Sun, Egg and Cap stood still at one of the test moments.
  All 122 tests pass now, covering all eleven motifs.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.24.0] – 2026-11-08
### Added
- "Dark widgets in dark mode" (Settings → Widgets, off by default): light paper turns dark in dark
  mode, the day's colour stays; the list widget gets a dark card. On Android 12+ each widget carries
  a light and a dark picture and the launcher switches live with the phone; older Android uses the
  mode at the last redraw.
- "Use the phone's colours (Material You)" per day (Look → Colours, Android 12+): the phone's accent
  and neutral colours instead of the day's own, light and dark. Picked up at the next redraw
  (midnight or any change) after a new wallpaper. Carried in backups.
### Tests
- `DarkLookTest`: dark paper rule, the launcher shows the dark picture in dark mode (views applied in
  a night configuration) and the same picture when switched off, dark list, phone colours only when
  asked for; backup round trip. Watched failing on planted faults (only the light picture, dark mode
  doing nothing, phone colours always on, field dropped from backups).
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.23.0] – 2026-11-08
### Added
- Your own photo on a mark day (Look → Photo → Pick photo; the phone's photo picker, no permission).
  Stored in the app's own folder, scaled down to at most 900 px.
- Polaroid shows the photo in its picture area, white numbers over a soft shade.
- New template "Photo": the photo fills the card, countdown and name in white over a shade (wide:
  shade on the text side). Without a photo, a gradient in the day's colour. Picking a photo on another
  template switches to Photo. `docs/photo.png`.
- Photos stay on the phone: never in a backup (no field, file name or image data); restored days have
  no photo and draw as without one. The export message says so. A replaced photo, a removed one and
  a deleted day's photo are deleted at once; leftovers are cleaned up later.
### Tests
- `PhotoTest`: stored small (4000×3000 → 900), replaced/deleted photos removed, no photo in a backup
  and the restored day still draws, photo inside the shape and never at the edge, white text readable
  on a white photo. Watched failing on planted faults (photo in the export, no downscaling, photo not
  clipped, no shade, photo left after deleting the day).
### Moved
- More motifs, Material You and dark mode move to 0.24 (roadmap).
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.22.1] – 2026-11-08
### Added
- "What's new" button next to Settings on the main screen: the last 10 versions in plain words
  (Danish/English), newest first, each with "Try:" – where to find it. A dot on the button until this
  version's news has been opened. `docs/whats-new.png`.
- The list lives in `ui/WhatsNew.kt` and must start with the app's own version: a test fails if
  versionName is raised without a new entry.
### Tests
- `WhatsNewTest`: newest entry = versionName, ten versions newest first, both languages, the dot
  goes away once opened (with screenshot). Watched failing with the list not updated.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.22.0] – 2026-11-08
### Added
- Optional time of day per mark day (Details, under the date; the phone's own time picker). The last
  24 hours then count down to that time instead of to midnight: hours, and minutes (in 5s) in the
  last hour; "Today!" from the moment itself. The date shows it: "lør. 21. nov. · 19:30".
- Widgets redraw exactly when the countdown needs it: when it starts (24 h before), every full hour,
  when the last hour begins, every 5 minutes in the last hour, and at the time itself; otherwise at
  midnight as before. Still one inexact alarm (no exact-alarm permission). Carried in backups.
### Changed
- Days without a time also count minutes in the last hour before midnight ("30 min").
### Tests
- `TimeOfDayTest`: counting to the time (days → hours → minutes → today), midnight without a time,
  the date with the time, every redraw moment; backup with time. Watched failing on planted faults
  (counting to midnight, no minutes, no 5-minute redraws, time dropped from backups).
### Not verified
- On the phones: inexact alarms may come a few minutes late in battery saving, so the minutes can lag.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.21.0] – 2026-11-08
### Added
- "Browse the coming days": a small or wide widget that shows the next day per tap, round and
  round; dots under the shape show where you are; back at the soonest day every new day. Offered when
  placing a widget and in Settings → Widgets. Only the tapped widget changes.
- On the day itself, tapping a widget opens a small menu: 📞 Call and 💬 Text (when the day has a
  phone number), ✓ Celebrated, Open. Call opens the dial screen (no call permission), Text a new
  message. One-time events have no "Celebrated".
- Phone number per day (Details → Phone, optional), typed or picked with the system's contact
  picker (only the chosen number is shared – no contacts permission). Carried in backups.
- "✓ Celebrated" marks the day as done for this year: the widget shows next year's day (365 days)
  and stops the party effect; the day after and next year are as always. Carried in backups.
### Changed from the roadmap
- No buttons laid over the widget picture (cannot be placed exactly on every launcher): the menu on
  the day instead. No automatic flipping (one bitmap per day hits the widget memory limit): browse by tap.
### Tests
- `InteractionTest`: browsing order, wrap, reset each day, separate widgets; what each tap does (menu
  on the day, editor otherwise, browse broadcast, unique per widget); menu items and dial/text
  intents; celebrated rule; dots never cut. Backup round trip with phone and celebrated. Watched
  failing on planted faults (no wrap, no daily reset, no menu, no celebrated rule, no room for the
  dots, phone dropped from backups).
### Not verified
- No screenshot of the day menu (a dialog window Robolectric's screenshot does not capture).
  Contact picker, dial/text screens and browsing to be checked on the phones.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.20.0] – 2026-11-08
### Added
- The day before, widgets count down in hours ("14 timer"); while a day is tomorrow they refresh
  every full hour (one inexact alarm, otherwise still once at midnight). The list widget keeps days.
- Dates show the weekday: "tors. 24. dec." (with the year when it is next year).
- Round birthdays (10, 18, 20, 25, 30 … 75 …) get 🎉 after the age; wedding anniversaries 25 🥈,
  40 ❤️, 50 🥇, 60 💎. On the day itself they get confetti (anniversaries: hearts) if no effect is
  chosen. Also in the list widget and the reminders.
- "Show how far it is to the day" (Decorate tab): a gold bar along the inside of the edge, as far
  round as the wait is over. Not on Minimal (no body). `docs/progress.png`.
### Tests
- `WidgetExtrasTest`: hours on the last day, hourly refresh only the day before, weekday dates in
  Danish/English, milestones and their automatic effect, the bar shows and never draws outside the
  shape. Watched failing on planted faults (no hours, no hourly refresh, no automatic effect, bar
  not clipped). An early edge check gave false alarms on the calendar's corners and was replaced by
  the stricter "never outside the shape".
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.19.0] – 2026-11-08
### Added
- Morning reminders: a notification on the day ("🦄 Clara 11 – today!"), or also the day before
  ("🎄 Jul – tomorrow"). Per day in the editor (Details → Reminder: off / on the day / also the day
  before; default on the day). Switched on in Settings → Widgets (off until then; asks for the
  notification permission on Android 13+), with the time 07/08/09/12/18:00 (default 08:00).
- One inexact, doze-tolerant alarm a day (no exact-alarm permission), planned again after each run,
  at midnight, after boot and on every widget refresh. Shown at most once a day. Tap opens the day.
- Backups carry the per-day choice; older backups get "on the day".
### Tests
- `ReminderTest`: which days are due (today/tomorrow per choice), alarm time, only planned when
  switched on, once a day, nothing without permission; backup round trip. Watched failing on
  planted faults (day-before ignored, shown twice a day, planned while off, field dropped).
### Not verified
- On a phone: delivery on time with battery saving (inexact alarms may come a little late).
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.18.0] – 2026-11-08
### Added
- "Always the next mark day": a small or wide widget can follow the calendar instead of one day.
  It moves on to the next day by itself at midnight (today counts; passed one-time events never).
  Offered first when placing a widget, and in Settings → Widgets to put one on the home screen.
- List widget "Next mark days" (resizable, 3×2 by default): as many coming days as fit (1–6) –
  emoji in the day's colour, name in the day's font (with age), weekday and date, days left, and a
  "Today!" pill on the day. Drawn as one bitmap; a transparent tap area per row (same proportions)
  opens that day, the title opens the app. In Settings → Widgets to put it on the home screen.
- `docs/ROADMAP.md`: plan for the other widget ideas (notifications, hours on the last day, weekday,
  progress ring, round birthdays, browse/quick actions/"celebrated", more motifs, own photo,
  Material You, dark mode).
### Tests
- `ListWidgetTest`: next-day binding over time, soonest-first list, rows that fit, tap areas lie on
  the drawn rows, each row's tap is its own intent, never cut by the edge. Watched failing on planted
  faults (title tap area weight changed, passed events not filtered, rows sharing one intent).
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.17.0] – 2026-11-06
### Added
- "How many times" for animated templates: all the time (default, as before), once, 3 or 5 times.
  The launcher starts the picture from the beginning every time the widget is shown (unlocking,
  going home – read in Android's own `ProgressBar.onVisibilityAggregated`), so a number means "that
  many loops each time you look, then the still picture". Switching pages on the home screen does not
  count as being shown again.
- How: the repeat count lives in the animation file and cannot be changed on a widget, so
  `scripts/motifs.py` now writes a 1×/3×/5× variant of every picture (every animation ends after
  exactly n loops, back in the still pose) and the eight widget layouts that use them.
- The editor preview plays the chosen number of loops and starts again when the choice changes.
  Backups carry the choice; older backups get "all the time".
### Fixed
- Segmented choices in the editor ("Den sidste uge", "Hele tiden") shrink a little to fit instead
  of being cut off with "…".
### Tests
- `finiteLoopsEndTogether` (every variant: same motion, all animations end after n loops, ends
  still), `widgetPlaysTheChosenNumberOfLoops`, `pictureStartsAgainWhenShownAgain` (Android's
  ProgressBar code, not the launcher), backup and editor cases. Each watched failing on a planted
  fault first (repeat count one too high, 3× mapped to the 1× layout, field dropped from JSON,
  no hide/show).
### Not verified
- Not seen on Samsung/Oppo: whether their launchers restart the picture on unlock as Android's code does.
### Published
- Uploaded to MarkdaysReleases on the owner's request (2026-11-06); public link verified.
- Owner confirmed on a OnePlus 11 and a Samsung S25 (2026-11-08): animations work.

## [0.16.0] – 2026-11-06
### Added
- Six animated templates – Cake, Balloons, Gift, Heart, Fireworks, Snow – like a weather widget: a
  round picture next to the countdown. On the home screen the picture moves (flames flicker,
  balloons sway, the lid hops, the heart beats, fireworks burst, snow falls). The rest of the look
  (colour, pattern, font, text colours, effects) works as on the other templates.
- How it moves: home-screen widgets cannot run Lottie or redraw many times a second. Each picture is
  an animated vector in an indeterminate ProgressBar laid exactly over the empty square of the widget
  bitmap (padding from the same layout maths; one layout per real size on Android 12+). The launcher
  plays it on its render thread, only while the widget is visible, and "Remove animations" shows the
  still picture. Pictures are generated by `scripts/motifs.py`; every loop starts and ends in the still pose.
- "The picture moves": always, in the last week (default) or only on the day; otherwise the still
  picture is drawn into the bitmap. Settings → "Animations on the home screen" turns all motion off.
- Editor: an "▶ Animated" row in the template picker (thumbnails move), the preview moves when the
  widget does, and explains when it will ("Snow moves on the day itself (in 48 days)", or that
  animations are off). Three new style ideas: Cake party, Snowy, New Year.
- Backups carry the new setting; older backups get "the last week".
- Tests: `MotifAudit` (pictures move, loop without a jump, start in the still pose, never leave their
  square, repeat forever) and `MotifWidgetTest` (the moving picture lands on the still one within
  a pixel, only the square is left empty, motion follows the setting and the chosen time, portrait
  and landscape layouts). Each was watched failing on purpose-made faults first. `docs/animated.png`.
### Not verified
- No emulator here: whether Samsung's and Oppo's launchers play the animation is only visible on the
  phones. If a launcher does not, it shows the still first frame.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.15.3] – 2026-11-05
### Fixed
- Snow on round shapes (Ring, Bubble, Arch, Blob) was a small lump on the very top. The cap is now
  the shape lifted a little minus the shape pushed a little down – the crescent snow forms on a
  ball: thickest on top, thinning down the curved sides, following any outline. Mounds and drips are
  placed along the outline itself (PathMeasure) where it faces up, turned with the curve; drips are
  fewer and rounder. A cool shade underneath keeps white snow visible on white shapes.
### Added
- Test `snowCoversTheTopOfTheShape`: the largest connected piece of snow must span at least 60 %
  of the shape's width (single flakes do not count). It failed on the old snow for Ring, Bubble,
  Arch and Blob (51–54 %) and passes now; `snowStaysWithinTheShape` and the edge audit still pass.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request); public link serves 0.15.0.

## [0.15.2] – 2026-11-05
### Fixed
- Snow stuck out past the shape and floated as a dotted line above it. It is now the shape's own
  top edge, lifted slightly and cut off with a soft wavy, dripping lower edge, so it follows rounded
  corners, circles, the arch and the blob and is never wider than the shape; a soft lumpy ridge
  (one union, no holes) on the flat part of the top; flakes fall only above the shape.
  Minimal (no body) gets falling snow instead of a cap.
- Effects now follow the exact shape of Arch, Blob and the tilted Polaroid (new `Outline.shape`),
  so glow and rainbow borders hug them too.
### Added
- Test `snowStaysWithinTheShape` (all templates, small and wide; watched failing with the cap made
  wider than the shape). `docs/snow.png` close-ups.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request); public link serves 0.15.0.

## [0.15.1] – 2026-11-05
### Fixed
- The editor preview always drew the chosen effect, so a day with e.g. snow "only on the day" showed
  snow in the preview but not on the home screen. The preview now shows exactly what the widget shows
  today; an effect that comes later is explained underneath ("Snow shows on the day itself
  (in 49 days)") with "See the day" to preview the day itself (number 0, effect on) and
  "Back to today". Template thumbnails no longer force the effect either.
- Test `effectsThatComeLaterAreExplainedNotShown`; screenshot test of the case.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request); public link serves 0.15.0.

## [0.15.0] – 2026-11-05
### Added
- Eight new templates (small and wide), drawn in `widget/ExtraTemplates.kt`:
  simple – Clean; special – Polaroid, Ticket, Arch, Neon; abstract – Blob, Shapes (Memphis), Aura.
  Each has its own effect outline, so effects stay inside the reserved margin.
- Nine new style ideas for them (Minimal, Memory, Travel, Sunset, Neon, Dream, Art, Bubbly, Garden).
### Changed
- Patterns are now scenes that rise from the bottom behind the number, in layers that fade upwards,
  tinted from the day's colour (white tones on dark surfaces): Gradient, Waves, Hills, Mountains,
  Clouds, Bubbles, Flowers, Hearts, Sprinkles, Stardust, Blobs. On the calendar sheet the scene rises
  in the paper below the header. Old stored names map to the closest new one
  (Dots → Bubbles, Stripes → Waves, Gingham → Hills).
- The editor shows patterns as cards with the day drawn in each pattern.
### Added (tests)
- `patternsRiseFromTheBottom` (centre of every pattern in the lower part; watched failing with the
  waves moved to the top), `everyTemplateLooksDifferent`; the edge audit now covers all 14 templates.
- `docs/templates.png`, `docs/effects.png`, `docs/patterns-fonts.png` updated.
### Published
- Uploaded to MarkdaysReleases on the owner's request (2026-11-05).

## [0.14.0] – 2026-11-05
### Fixed
- Effects were cut off by the edge of the picture (most visibly in the app and on tight
  launcher cells). Every effect now has a known margin (`Effects.margin`) that the renderer
  reserves while the effect is shown, and the drawings stay inside it. Guarded by
  `EffectAudit.effectsAreNeverCutByTheEdge` (all templates × effects, small and wide, at fill 100 %;
  watched failing with the confetti margin removed).
### Changed
- Effects redrawn: confetti denser at the top, golden glow with a finer gold border, gold/white
  sparkles, three drawn balloons tied to the corner (instead of emoji that were cut), hearts just
  outside the edge, snow lying on the top edge with drips, a cleaner rainbow border.
- Patterns redesigned to be subtle and laid out from the centre: Gradient, Dots, Sprinkles,
  Stripes, Gingham, Waves, Hearts, Stars. "Lined" and "Squared" were removed (stored days fall back
  to no pattern). Presets updated (Pastel: gradient, Party: sprinkles, Sea: waves, Cosy: dots).
- `emojiStaysOnTopOfEffects` now compares renders with the same layout (an active effect shrinks
  the drawing to make room); it still fails when an effect is drawn over the emoji.
- `docs/effects.png`, `docs/patterns-fonts.png` updated.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request); public link serves 0.10.0.

## [0.13.0] – 2026-11-05
### Changed
- Friendlier editor:
  - The widget preview stays on screen; the form is split into tabs
    (📝 Details · 🎨 Look · ✏️ Text · ✨ Decorate) with a short slide between them.
  - Style ideas: ten complete looks in one tap (Classic, Pastel, Party, Elegant, Cosy, Christmas,
    Love, Night, Sea, Retro), each previewed with the user's own day; "Reset look".
  - Emoji suggestions per kind (and season for holidays) first, all emoji behind "Show all".
  - Colours as one sideways-scrolling row instead of big grids; text colours explained.
  - Only relevant switches: "follows Easter" for holidays, "show age" for birthdays/anniversaries,
    no "year known" for one-time events.
  - "Discard changes?" when closing (✕ or back) with unsaved changes; nothing is asked for an
    untouched new day.
  - Clear button texts: "Add mark day" / "Save changes"; new days get "Give it a look →";
    home-screen actions only for saved days.
### Added
- Tests: presets apply and keep the day, relevant switches, discard guard (watched failing with
  the check disabled), emoji suggestions, tabs keep the form. `docs/app-editor.png` shows every tab.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request); public link serves 0.10.0.

## [0.12.0] – 2026-11-05
### Changed
- The whole app UI is rewritten in Jetpack Compose with Material 3 (BOM 2025.05.01) – the old
  View screens (spinners, checkboxes, list dialogs) are gone. Data layer and widget renderer unchanged.
  - Edge to edge, large rounded surfaces, Fredoka (bundled) for headlines, light/dark brand
    scheme plus optional Material You colours from the wallpaper (Settings).
  - Home: greeting, a big "Next up" card in the day's own colour with a number that counts up and
    the widget tilted beside it, then the list grouped Soon / Within 30 days / Later / Passed with
    countdown pills; collapsing large top bar; extended FAB that shrinks on scroll.
  - Adding a day: bottom sheet with gradient tiles and one-tap holidays; confetti burst and a
    snackbar (pin / undo). Long-press opens an actions sheet (existing widget, pin, edit, delete with undo).
  - Editor: live preview on a soft wallpaper with the countdown sentence, section cards, filter
    chips, switches, Material date picker, template and font cards that show the real result,
    colour circles with checks, segmented buttons, haptic ticks, fixed Save button.
  - Settings, widget tuning and widget picker in the same style; predictive back enabled;
    themed (monochrome) launcher icon.
- Editor logic moved into a plain `EditorForm` (unit tested).
### Added
- Tests: `EditorFormTest` (every kind of day survives the editor unchanged, defaults per kind,
  one-time events keep their year); screenshots of all screens in light and dark
  (`docs/app-screens.png`, `docs/app-editor.png`).
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request); public link serves 0.10.0.

## [0.11.0] – 2026-11-05
### Added
- Light and dark app theme (Material 3 colour scheme in raspberry/rose; `values-night`), chosen in
  Settings: Auto (follow the phone) / Light / Dark (`AppTheme`, applied at start in `MarkdaysApp`).
- Settings screen (gear in the top bar): theme, language, adjust widgets, backup export/import,
  about with version and font licences. Replaces the old ⋮ menu.
- New-day flow: "What do you want to celebrate?" sheet with Birthday / Anniversary / Holiday /
  Event tiles and 10 one-tap holidays (Christmas Eve, New Year's Eve, Easter, Shrovetide,
  Ascension, Whitsun, Midsummer Eve, Halloween, Valentine's Day, Father's Day); already added
  ones are ticked. Each kind starts with fitting defaults (e.g. birthday: age + confetti on the
  day; event: one-time + sparkle the last week) and its own name hint.
- Editor in section cards (What, When, Template and colours, Text, Emoji and effect, Home screen),
  a countdown sentence under the preview ("Clara turns 11 in 65 days"), the keyboard opens for
  the name, Done opens the date picker, Save is always visible, and a new day asks for its date
  instead of saying "turns 0 today".
- After adding: "🎉 Clara added – in 65 days" with "📌 Home screen" (or Undo for one-tap holidays).
- Friendly empty state; extended "New mark day" button that shrinks while scrolling.
- `UiTest`: theme choice applied, holiday dates, kind defaults, settings opens; light/dark
  screenshots via Robolectric (`docs/app-screens.png`).
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request); public link serves 0.10.0.

## [0.10.0] – 2026-11-05
### Added
- Text colours: "Text colour – name" and "Text colour – number", each Automatic (contrast, as before),
  14 presets or a custom colour. Picked colours are drawn fully opaque.
- Other fonts: the phone's own system fonts that can write Danish letters (Android `SystemFonts`),
  shown in their own font, and importing a .ttf/.otf file (copied into the app). Fonts installed via
  Samsung's "font style" are private to Samsung and cannot be used by other apps.
  A missing custom font falls back to the chosen built-in font; imported font files are not part
  of a backup.
- Tests: text colours appear (caught that Card drew the picked name colour semi-transparent),
  imported font used / missing font falls back (watched failing with custom fonts ignored),
  backup carries pattern, custom font and text colours.
### Published
- Uploaded to MarkdaysReleases on the owner's request (2026-11-05).

## [0.9.0] – 2026-11-04
### Fixed
- Effect borders were drawn over the emoji and clipped it. Emoji are now drawn last
  (`emojiStaysOnTopOfEffects`, watched failing with the old order: 412 of 2607 emoji pixels covered).
### Added
- 13 more fonts: Medium, Extra bold and 11 bundled Google Fonts (SIL OFL 1.1, license in
  `assets/licenses/OFL-fonts.txt`): Pacifico, Dancing Script, Lobster, Caveat, Comfortaa,
  Playfair Display, Bebas Neue, Fredoka, Amatic SC, Righteous, Quicksand. Same look on every phone.
- 11 more paper colours (18 in all) and paper patterns: dots, stripes, gingham, lined, squared,
  hearts, stars – on every template's paper surface; included in "use on all" and backups.
- `docs/patterns-fonts.png`.
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request).

## [0.8.0] – 2026-11-04
### Added
- ⋮ → Language: Automatic (phone language) / Dansk / English. Uses AppCompat per-app locales
  (on Android 13+ also in the phone's settings → Apps → Markdays → Language, via `locales_config.xml`).
  Widgets, dates, country names and first-run example days ("Christmas Eve"/"Easter" or "Jul"/"Påske")
  follow the choice (`Lang.localized`, since widgets are drawn outside activities).
- `LangTest` (watched failing with the choice ignored).
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request); public link still serves 0.6.0.

## [0.7.0] – 2026-11-04
### Added
- All country flags as emoji: "🏳️ Flag" in the editor opens every ISO 3166 country (≈250) named in the
  phone's language, with search. 🇩🇰 and a few celebration emoji added to the presets.
- Effects per mark day: confetti, golden glow, sparkle, balloons, hearts, snow, rainbow border –
  drawn along each template's outline – shown always, the last week, or only on the day.
  The editor preview always shows the chosen effect. Overview: `docs/effects.png`.
- Tests: flag codes/names/search, effect timing, every effect changes the drawing (and "none" does
  not), backup carries effect settings.
### Not published
- Not uploaded to MarkdaysReleases: the owner publishes only on explicit request.

## [0.6.0] – 2026-11-04
### Added
- ⋮ → "Adjust widgets" (`TuneActivity`): per-phone sliders for small/wide widget size, calendar
  sheet height, name text size, number size, emoji size, and placement (top/middle/bottom), with a
  preview at the real widget size of this phone and immediate update of the home-screen widgets.
  Replaces the old five-step "Widget size" menu. Included in backups (older backups still import).
- Long names are first condensed (up to 15 % narrower) before the font is made smaller.
- Tests: tuning survives backup round trip, old backups import, top/bottom placement,
  taller sheet (watched failing with the height ignored), tuning screen opens.
  `docs/tuning-compare.png`: default vs. tuned.

## [0.5.0] – 2026-11-04
### Added
- Backup: ⋮ → Export backup / Import backup (JSON via Android's file picker: Drive, Downloads …).
  Carries every mark day with its look and the widget-size setting, so users can move to a
  differently signed build (e.g. Google Play). Import can add (skipping days already present)
  or replace all. Widget placements are not part of a backup (Android gives new widget ids).
- "Show on a widget you already have": switch what an existing home-screen widget shows, from the
  list (long-press) or the editor. Apps cannot choose the home-screen page for a new widget, so
  placing widgets once and switching their content avoids dragging them across pages.
- Tests: `BackupTest` (round trip of every field – watched failing with the template field removed –,
  add-mode skips duplicates, no double seeding, invalid files rejected without data loss),
  `ExistingWidgetTest`.

## [0.4.0-signing] – 2026-11-04
### Added
- `scripts/publish-release.sh` refuses to publish an APK whose signing certificate is not the one
  of the published 0.4.0 (SHA-256 `abdae94d…`); watched refusing a re-signed APK (exit 1).
- Build uses `signing/markdays-test.keystore` when present. The key itself is **not** committed:
  pending the owner's decision (blocked by the session's credential filter).

## [0.4.0] – 2026-11-04
### Added
- Public test downloads: `scripts/publish-release.sh` builds, tests and publishes the APK to
  github.com/renegreth/markdaysreleases (`Markdays-latest.apk`, `version.json`). App version set to 0.4.0 (build 4).
- Six templates for both widget sizes: Calendar, Card, Ring (fills up as the day approaches),
  Bubble, Glass and Minimal. Picked per mark day in the editor with live thumbnails;
  "use on all" now includes the template. Overview: `docs/templates.png`.
- Put a widget on the home screen from the app (`requestPinAppWidget`): buttons in the editor and
  long-press in the list. `PinReceiver` binds the new widget to the mark day.
- Widget picker shows rendered previews (`drawable-nodpi/widget_preview_*.png`, Danish).
- Tests: progress ring maths (`ProgressTest`), pin callback binds / ignores invalid ids,
  every template renders pixels in both sizes.
### Changed
- The wide widget is drawn as a bitmap too (`WidgetRenderer` replaces `SheetRenderer`); old XML sheet
  layouts and drawables removed. The app shows the bitmaps directly (no in-app RemoteViews any more).

## [0.3.1] – 2026-11-04
### Fixed
- App crashed on start (0.3.0): list badges and the editor preview inflated the widget RemoteViews
  with the AppCompat activity context, which turns ImageView into AppCompatImageView, and
  RemoteViews refuses `setImageBitmap` on it. Now inflated with the application context.
### Added
- Robolectric smoke tests (`LaunchTest`: main screen, editor, widget update) – reproduced the crash
  before the fix. `RenderSnapshot` renders the 1×1 sheet to PNG (`docs/widget-render.png`).
- Google's Maven Central mirror for Gradle and Robolectric downloads (Maven Central returned HTTP 429).

## [0.3.0] – 2026-11-04
### Fixed
- 1×1 widget on Samsung One UI: the launcher's rounded clipping cut into the calendar sheet, and the
  sheet kept a fixed size when the widget was resized. The sheet is now drawn as a bitmap
  (`SheetRenderer`) at the widget's real size with a transparent margin, keeps its proportions and
  grows/shrinks with the widget (redrawn in `onAppWidgetOptionsChanged`).
### Added
- "Widget size" in the main menu (extra small … fill, default medium = 80 % of the widget area).

## [0.2.0] – 2026-11-04
### Added
- Per mark day look: any header colour and paper colour (20 + 8 presets plus a custom
  hue/saturation/brightness picker), 11 built-in fonts, 48 emoji presets, emoji size (none/small/medium/large).
- Text colour switches automatically between white and dark for contrast.
- Live preview of both widgets at the top of the editor; list badges are rendered from the same widget views.
- Menu action "Use paper, font and icon size on all".
- `docs/mockup-customize.png`.
### Changed
- Widget sheet drawn from white masks tinted at runtime (`setColorFilter`) instead of six fixed header drawables.
- Stored colours are ARGB; older saved colour names are migrated on read.

## [0.1.2] – 2026-11-04
### Fixed
- Widgets stretched to the full launcher cell height and looked too tall. The 1×1 sheet now has a
  fixed 64×72 dp size and the 3×1 board a fixed 80 dp height, both centred in the cell.

## [0.1.1] – 2026-11-04
### Fixed
- Compile error in the colour picker (`color` shadowed by `GradientDrawable.color`).
### Added
- `docs/mockup.png` design mock-up of widgets and list.

## [0.1.0] – 2026-11-04
### Added
- First version of the Android app: list, create, edit and delete birthdays and other mark days.
- 1×1 calendar-sheet widget (name + age header, days left, emoji icon) and 3×1 note widget
  (days left, date, title). Widget picks a mark day on placement and can be reconfigured.
- Yearly or one-time dates, Easter-relative dates, leap-day handling, optional age display.
- Daily refresh after midnight plus refresh on boot, app update, time and time-zone change.
- Danish and English strings. Christmas Eve and Maundy Thursday seeded on first run.
- JVM unit tests for the date logic (`DayCalcTest`).

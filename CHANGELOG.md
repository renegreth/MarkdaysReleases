# Changelog

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

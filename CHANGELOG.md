# Changelog

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
### Not published
- Not uploaded to MarkdaysReleases (owner publishes only on request); public link serves 0.10.0.

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

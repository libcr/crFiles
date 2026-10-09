# crFiles

A desktop file manager built on Chromium 150 Views, with Chrome-style tabs, flexible split panes, file previews, and nearby file sharing. crFiles brings browsing, organizing, and transferring files together in one workspace on Linux and Windows.

## Download

- **Windows:** [Microsoft Store](https://apps.microsoft.com/store/detail/9NCC8M0F2D2W?cid=DevShareMCLPCS)
- **Linux and macOS:** [Download from GitHub Releases](https://github.com/libcr/crFiles/releases)

## Screenshots

**Tabs, nested split panes, and folder bookmarks**

![crFiles with multiple tabs, nested split panes, bookmarks, and a floating pane toolbar](Screenshot%20From%202026-09-25%2009-43-15.png)

**Icon view with image thumbnails**

![crFiles browsing screenshots in a compact icon grid with image thumbnails](Screenshot%20From%202026-09-25%2010-04-49.png)

**Content search with highlighted matches**

![crFiles search tab showing a query chip, pause control, content snippets, highlighted matches, and open-folder actions](Screenshot%20From%202026-09-26%2009-54-54.png)

The screenshots show the application on Linux. The search screenshot shows the current search interface; details in older screenshots may differ from the latest source.

## Browse your way

- **Multiple tabs:** Chrome-style tabs integrated into the title bar, with independent folder navigation.
- **Four-way splits:** Open a folder in a new split to the left, right, top, or bottom. Nest splits and drag their dividers to resize them.
- **Active-pane navigation:** The shared breadcrumb bar, editable address field, and view controls follow the selected pane.
- **Editable breadcrumbs:** Click a segment to navigate, or double-click the navigation bar to enter a path. Press Enter to navigate or Escape to return to breadcrumbs.
- **Saved workspaces:** Restore tabs, split layouts, pane names, paths, view preferences, column widths, and scroll positions at the next launch.
- **Collapsible sidebar:** Drag the sidebar down to zero to hide it, then drag it out from the window edge. Double-click the edge to restore its previous width, or use Ctrl+L.
- **Bookmarks:** Pictures and Videos are provided initially. Drag a folder into the bookmark area to add it. Bookmarks support opening in a new tab, renaming, removal, and properties.
- **Useful locations:** Home, Desktop, Downloads, and crFiles Trash. Received files appears only when its configured directory exists.

On Windows, local navigation paths are displayed as `/c/Users`. The virtual `/` location lists available drives, and Up from a drive root returns to that list. Native paths such as `C:\Users` and `C:/Users` are also accepted. File operations and copied paths continue to use Windows-native paths; UNC paths retain their native representation.

## List and icon views

Switch between a detailed list and a compact icon grid using the integrated view toggle.

- Choose icon sizes of **22, 32, 48, 64, 96, or 128 pixels** using the slider or Ctrl+Plus / Ctrl+Minus.
- Sort by name, modification time, size, or file type, with folders before files.
- Show or hide hidden files and choose visible list columns.
- Resize list columns by dragging their header dividers.
- Select items with Ctrl-click, Shift range selection, or a selection rectangle. Ctrl+A toggles selection of all displayed entries. With the folder view focused, press A–Z to jump to the next item starting with that letter; repeated presses wrap around.
- See the combined size of selected files in the pane status area.

File-type icons use bundled SVG assets selected by MIME type, without scanning the system icon directory at runtime. Icon view provides image thumbnails, including SVG, and **PDF first-page previews** through PDFium. Previews preserve aspect ratio; unavailable previews fall back to file-type icons.

Double-clicking a file opens it in the system's default application. The Open With menu offers available application associations.

Large folders use virtualized rows, background directory loading, cached sorting keys, and bounded directory and thumbnail caches. Preview work prioritizes visible entries, limits concurrency, and discards canceled results after navigation.

## Organize files

The context menu provides Cut, Copy, Paste where available, Move to, Copy to, Rename, ZIP compression, Move to Trash, Open in Terminal, Copy File Path, and Properties. Folders can also open in a new tab or a split pane.

Drag files and folders between panes, or onto folders within a pane, to **move** them. Adding a bookmark by dragging a folder into the sidebar does not move the folder itself.

Each pane has a floating toolbar with sharing, folder creation, and pane controls. Automatic toolbar hiding and folder transition animations can be configured in Settings.

### Private Trash

crFiles maintains its own Trash, separate from the operating system's recycle bin.

The Trash page has a centered capsule toolbar with **Restore** and **Empty Trash**. Restore uses the saved original path and does not overwrite an existing destination. Empty Trash permanently removes crFiles Trash contents after confirmation in an anchored popover; clicking outside the popover cancels it.

## Nearby sharing

Send files and folders to nearby devices through **Share to** in the context menu. The dialog shows discovered devices, transfer information, and circular progress indicators.

- **Local discovery:** mDNS discovery on the local network, with a manual connection option.
- **crPhotos compatibility:** Uses the crPhotos desktop discovery and authenticated transfer protocol. Folder transfers and named pane targets require peers that support the crFiles extensions.
- **Device verification:** Pairing-code confirmation and encrypted TLS transfers.
- **Trusted devices:** A green badge identifies trusted peers. Manage saved trust from the title-bar menu; automatic acceptance from trusted devices is configurable.
- **Shared panes:** Enable the Share toggle on a pane to advertise its folder as a receive target. Shared targets have persistent identities and can be renamed.
- **Targeted receiving:** Incoming confirmation prompts appear near the target pane when it is visible, or near the main window's lower-right corner otherwise.
- **Transfer results:** Completion popovers summarize the transferred size and elapsed time.

A shared target remains attached to the folder selected when sharing was enabled, even if the pane later navigates elsewhere. A custom-named pane receives directly into its target folder; default receiving can use separate `Received-*` batch folders.

Nearby discovery and receiving are enabled by default and can be changed in **Settings → Nearby sharing**, along with the device name, avatar, receive directory, and trusted-device acceptance preference.

Desktop sharing targets local IPv4 networks. Remote folder browsing is not implemented. Windows receive targets currently require local drive paths; UNC paths, junctions, and symbolic links are not supported as receive targets.

## Search folders

Click **Search** in a pane’s floating toolbar to open a dedicated tab for that folder and its descendants. The integrated search field supports **Search by Path** (the default) and **Search by Content**. Its filter menu also includes **Hidden File**; enabling it adds hidden results without rereading ordinary files.

Type an extension followed by Space, such as `.pdf ` or `.jpg `, to add a removable file-type chip. Multiple extensions are alternatives. Type a query and press Enter to start searching; only then does the query become a chip. Changing the search mode with a query already present starts a new search. Matching is case-insensitive.

Path search shows matching paths on one line. Content search shows each filename and a highlighted excerpt on two lines. Content sources include UTF-8 and UTF-16 text, embedded PDF text, and JPEG, PNG, WebP, and TIFF metadata such as EXIF camera details, dates, descriptions, and GPS fields. Search does not perform OCR or image recognition.

The search tab shows live match and scan counts, with a pause/resume icon beside the search root. Removing the query chip or pressing Escape cancels the task. Double-click a result to open it, or use its folder icon to open the containing folder and select the matching file. Results use a virtual list, so large result sets do not create a view for every match. Enumeration and parsing run in a separate Mojo search process with cooperative pause and cancellation. Searches are bounded and do not create a persistent content index; protected, unsupported, or oversized files may be skipped or partially searched.

## History and settings

Open **History** from the title-bar menu to view a dedicated history tab. A local SQLite database records file operations, folder access, file opening, and incoming or outgoing transfers, including their source, destination, result, and interaction type where applicable.

Search by file path with matching text highlighted, or filter by Move, Move to Trash, Access, Open File, Send, and Receive. History is ordered by time.

Settings includes:

- **General:** Language, system/light/dark appearance, automatic toolbar hiding, and folder animations.
- **Nearby sharing:** Discovery, receiving, device identity, and trust-related preferences.
- **History:** Retention of 7 days, 30 days, 90 days, or 1 year, plus controls for which supported event types are recorded.

English is the source language. Translations are available for Simplified Chinese, Hong Kong and Taiwan Traditional Chinese, Arabic, French, Canadian French, Russian, Spanish, Latin American Spanish, Brazilian Portuguese, and European Portuguese. Language changes require a restart.

## Keyboard shortcuts

| Shortcut | Action |
| --- | --- |
| Ctrl+T | New tab |
| Ctrl+W | Close current tab |
| Ctrl+Tab / Ctrl+Shift+Tab | Next / previous tab |
| Ctrl+Q | Quit |
| Ctrl+L | Show or hide the sidebar |
| Ctrl+Plus / Ctrl+Minus | Increase / decrease icon size |
| Ctrl+= | Increase icon size |
| Ctrl+A | Toggle select all in the file view |
| A–Z (folder view focused) | Select the next item starting with that letter; repeat to cycle |
| Ctrl+C / Ctrl+X / Ctrl+V | Copy / cut / paste |
| Alt+Left / Alt+Right | Back / forward |
| F5 | Refresh |
| F11 | Toggle fullscreen |
| Enter | Open a focused item or submit an edited path |
| Escape | Cancel path editing |

Numeric-keypad plus and minus are also supported with Ctrl. Icon-size shortcuts do not act while a text field has focus.

## Development

crFiles is a native Chromium Views application using the shared `libcr` windowing components, Skia for graphics, PDFium for PDF thumbnails, and SQLite for History. Building requires the corresponding Chromium 150 source workspace with `crFiles` and `libcr` integrated; this repository's README and screenshots are not a standalone build environment.

From an appropriately configured Chromium source root, use **autoninja**:

```sh
# Linux
autoninja -C out/debian crFiles

# Windows target, with a configured Windows toolchain/output directory
autoninja -C out/win10 crFiles
```

Output-directory names depend on the local build configuration. The current source contains both Linux and Windows implementations; platform-specific behavior and recent UI changes should be validated with the corresponding build.

# crFiles

A desktop file manager built on Chromium 154 Views, with Chrome-style tabs, flexible split panes, file previews, and nearby file sharing. crFiles brings browsing, organizing, and transferring files together in one workspace on Linux, Windows, and macOS.

## Download

- **Windows:** [Microsoft Store](https://apps.microsoft.com/store/detail/9NCC8M0F2D2W?cid=DevShareMCLPCS)
- **Linux and macOS:** [Download from GitHub Releases](https://github.com/libcr/crFiles/releases)

## Screenshots

**Android Quick Share: device selection and pairing-code comparison**

![crFiles Quick Share dialog sending 18 selected files to an Android phone, waiting for acceptance and displaying a pairing code](Screenshot%20From%202026-10-15%2019-33-56.png)

**Android Quick Share: transfer results**

![crFiles Quick Share result showing 18 files sent and warning that the receiving device has not confirmed delivery](Screenshot%20From%202026-10-15%2019-34-06.png)

**Tabs, nested split panes, and folder bookmarks**

![crFiles with multiple tabs, nested split panes, bookmarks, and a floating pane toolbar](Screenshot%20From%202026-09-25%2009-43-15.png)

**Icon view with image thumbnails**

![crFiles browsing screenshots in a compact icon grid with image thumbnails](Screenshot%20From%202026-09-25%2010-04-49.png)

**Content search with highlighted matches**

![crFiles search tab showing a query chip, pause control, content snippets, highlighted matches, and open-folder actions](Screenshot%20From%202026-09-26%2009-54-54.png)

The screenshots show the application on Linux. The October 15 screenshots show Quick Share pairing and transfer results. Sent bytes do not by themselves confirm delivery; check the received files when the device does not acknowledge completion. Details in older screenshots may differ from the latest source.

## Browse your way

- **Multiple tabs:** Chrome-style tabs integrated into the title bar, with independent folder navigation. Drag tabs to reorder them, pin frequently used tabs, and use the tab context menu to close other unpinned tabs.
- **Four-way splits:** Open a folder in a new split to the left, right, top, or bottom. Nest splits and drag their dividers to resize them.
- **Active-pane navigation:** The shared breadcrumb bar, editable address field, and view controls follow the selected pane.
- **Editable breadcrumbs:** Click a segment to navigate, or double-click the navigation bar to enter a path. Press Enter to navigate or Escape to return to breadcrumbs.
- **Saved workspaces:** Restore tabs, split layouts, pane names, paths, view preferences, column widths, and scroll positions at the next launch.
- **Collapsible sidebar:** Drag the sidebar down to zero to hide it, then drag it out from the window edge. Double-click the edge to restore its previous width, or use Ctrl+L.
- **Bookmarks:** Pictures and Videos are provided initially. Drag a folder into the bookmark area to add it. Bookmarks support opening in a new tab, renaming, removal, and properties.
- **Useful locations:** Home, Desktop, Downloads, and crFiles Trash. Received files appears only when its configured directory exists. macOS also provides an Applications location.

On Windows, local navigation paths are displayed as `/c/Users`. The virtual `/` location lists available drives, and Up from a drive root returns to that list. Native paths such as `C:\Users` and `C:/Users` are also accepted. File operations and copied paths continue to use Windows-native paths; UNC paths retain their native representation.

## List and icon views

Switch between a detailed list and a compact icon grid using the integrated view toggle.

- Choose icon sizes of **22, 32, 48, 64, 96, or 128 pixels** using the slider or Ctrl+Plus / Ctrl+Minus.
- Sort by name, modification time, size, or file type, with folders before files.
- Show or hide hidden files and choose visible list columns, including optional Created and Permissions columns where the platform supplies that metadata.
- Resize list columns by dragging their header dividers.
- Select items with Ctrl-click, Shift range selection, or a selection rectangle. Ctrl+A toggles selection of all displayed entries. With the folder view focused, press A–Z to jump to the next item starting with that letter; repeated presses wrap around.
- See the combined size of selected files in the pane status area.

File previews include images and SVG, **PDF first-page previews** through PDFium, HEIC/HEIF images, and static video frames. macOS uses native image/video support where available; Linux and Windows need suitable optional codec libraries for HEIC and HEVC. Missing codecs or unavailable previews fall back to file-type icons. Windows prefers native Shell icons, while macOS uses native application icons for app bundles; bundled MIME-type SVG icons provide fallbacks.

Icon sizes of 64, 96, and 128 pixels can show paper-style previews of recognized plain-text files, using up to the first five lines. **Settings → General → Preview images on hover** enables larger image previews in list and icon views; it is off by default.

Double-clicking a file opens it in the system's default application. The Open With menu offers available application associations. Optional single-click folder navigation is available in Settings. On macOS, opening an application bundle launches it; **Show Package Contents** browses inside it.

Large folders use virtualized rows, background directory loading, cached sorting keys, and bounded directory and thumbnail caches. Preview work prioritizes visible entries, limits concurrency, and discards canceled results after navigation.

## Organize files

The context menu provides Cut, Copy, Paste where available, Move to, Copy to, Rename, ZIP compression, Move to Trash, Open in Terminal, Copy File Path, and Properties. Folders can also open in a new tab or a split pane.

Drag files and folders between panes, or onto folders within a pane, to **copy** them while preserving the originals. Existing destination names are skipped without merging or overwriting. Adding a bookmark by dragging a folder into the sidebar does not move the folder itself.

Each pane has a floating toolbar with sharing, folder creation, and pane controls. Automatic toolbar hiding and folder transition animations can be configured in Settings.

### Archives and file operations

Create ZIP archives with progress and cancellation, or extract ZIP, 7z, RAR, TAR, TAR.GZ/TGZ, and TAR.XZ archives through **Extract here**, **Extract to same-name folder**, or **Extract to…**. Password-protected traditional ZIP and single-volume RAR are supported; AES-encrypted ZIP, encrypted 7z, and multipart RAR are not. Extraction prompts before replacing conflicting entries and records operations in History.

Same-filesystem moves use atomic renaming where supported. If a move falls back to copying across filesystems, crFiles retains the originals and reports incomplete movement; verify the destination before removing them. On macOS, ordinary copy/move operations preserve symbolic links and package metadata.

### Private Trash

crFiles maintains its own Trash, separate from the operating system's recycle bin.

The Trash page has a centered capsule toolbar with **Restore** and **Empty Trash**. Restore uses the saved original path and does not overwrite an existing destination. Empty Trash permanently removes crFiles Trash contents after confirmation in an anchored popover; clicking outside the popover cancels it.

## Android Quick Share

The Quick Share protocol implementation in crFiles comes from [crQuickShare](https://github.com/wuruxu/crQuickShare).

Right-click selected files or folders and choose **Quick Share** to send to an Android device on the same local network. Open the phone's Quick Share receive screen if it does not appear, compare the full pairing code on both devices, and accept the transfer. Linux also uses Bluetooth discovery and wake-up advertising when available; file transport still requires LAN connectivity.

- **Files and folders:** Send up to 100 files after recursively collecting selected folders. Empty folders are omitted, and Android determines its receiving location and handling of folder structure.
- **Progress and results:** View the current filename, per-file and total bytes, completed file count, speed, and remaining time. Results distinguish confirmed completion from files sent without a delivery acknowledgement.
- **Receiving:** Quick Share reception starts with crFiles. Each incoming transfer requires code comparison and acceptance; files are saved in a unique `Transfer-*` directory without overwriting existing files.
- **Independent settings:** **Settings → Quick Share** controls its enable switch (on by default), device name, and receive directory. The default on Linux is `~/Downloads/crFiles Received`.
- **Cancellation:** Closing the sending dialog keeps an active transfer running. Use Cancel in its session bubble to stop it.

## Nearby sharing

Send files and folders to nearby devices through **Share to** in the context menu. The dialog shows discovered devices, transfer information, and circular progress indicators.

- **Local discovery:** mDNS discovery on the local network, with a manual connection option.
- **crPhotos compatibility:** Uses the crPhotos desktop discovery and authenticated transfer protocol. Folder transfers and named pane targets require peers that support the crFiles extensions.
- **Device verification:** Pairing-code confirmation and encrypted TLS transfers.
- **Trusted devices:** A green badge identifies trusted peers. Manage saved trust from the title-bar menu; automatic acceptance from trusted devices is configurable.
- **Shared directories:** Enable the Share toggle to advertise a directory as a receive target. Tabs and splits showing the same directory share one toggle state and persistent target identity. Manage advertised directories from **Sharing folders** in the title-bar menu.
- **Targeted receiving:** Pairing, consent, progress, and results share a session bubble anchored to the directory or device. On macOS and Windows, background bubbles follow the tray icon or fall back to the screen work-area edge.
- **Transfer results:** Completion popovers summarize the transferred size and elapsed time.

A shared target remains attached to the folder selected when sharing was enabled, even if the pane later navigates elsewhere. Closing a tab or pane does not revoke the share. Transfers to an explicit shared directory write directly there; default receiving uses separate `Received-*` batch folders. Disabling a directory's share withdraws its target and cancels a transfer to it.

Desktop nearby sharing is disabled by default and can be changed in **Settings → Nearby sharing**, along with the device name, avatar, receive directory, and trusted-device acceptance preference.

Desktop sharing targets local IPv4 networks. Remote folder browsing is not implemented. Windows receive targets currently require local drive paths; UNC paths, junctions, and symbolic links are not supported as receive targets.

## Search folders

Click **Search** in a pane’s floating toolbar to open a dedicated tab for that folder and its descendants. The integrated search field supports **Search by Path** (the default) and **Search by Content**. Its filter menu also includes **Hidden File**; enabling it adds hidden results without rereading ordinary files.

Type an extension followed by Space, such as `.pdf ` or `.jpg `, to add a removable file-type chip. Multiple extensions are alternatives. Type a query and press Enter to start searching; only then does the query become a chip. Changing the search mode with a query already present starts a new search. Matching is case-insensitive.

Path search shows matching paths on one line. Content search shows each filename and a highlighted excerpt on two lines. Content sources include UTF-8 and UTF-16 text, embedded PDF text, and JPEG, PNG, WebP, and TIFF metadata such as EXIF camera details, dates, descriptions, and GPS fields. Search does not perform OCR or image recognition.

The search tab shows live match and scan counts, with a pause/resume icon beside the search root. Removing the query chip or pressing Escape cancels the task. Double-click a result to open it, or use its folder icon to open the containing folder and select the matching file. Results use a virtual list, so large result sets do not create a view for every match. Enumeration and parsing run in a separate Mojo search process with cooperative pause and cancellation. Searches are bounded and do not create a persistent content index; protected, unsupported, or oversized files may be skipped or partially searched.

## History and settings

Open **History** from the title-bar menu to view a dedicated history tab. A local SQLite database records file operations, folder access, file opening, and incoming or outgoing transfers, including their source, destination, result, and interaction type where applicable.

Search by file path with matching text highlighted, or filter by Move, Move to Trash, Access, Open File, Send, and Receive. History is ordered newest first, uses virtualized rows, and loads additional matches with Show more. Path filtering searches source and destination paths across the database.

Settings includes:

- **General:** Language, system/light/dark appearance, automatic toolbar hiding, folder animations, hover image previews, and single-click folder navigation.
- **Interface:** Minimal, underlined, or raised breadcrumb styles; system tray behavior on macOS and Windows; and an optional Windows-style titlebar on macOS.
- **Nearby sharing:** Discovery, receiving, device identity, and trust-related preferences.
- **Quick Share:** Android sharing, device name, and receive directory.
- **History:** Retention of 7 days, 30 days, 90 days, or 1 year, plus controls for which supported event types are recorded.

English is the source language. Translations are available for Simplified Chinese, Hong Kong and Taiwan Traditional Chinese, Arabic, French, Canadian French, Russian, Spanish, Latin American Spanish, Brazilian Portuguese, and European Portuguese. Language changes require a restart.

On macOS and Windows, the system tray is enabled by default. Closing the main window hides it while enabled sharing services and transfers continue. Clicking the tray icon toggles the window; Quit exits the application. Disabling the tray restores close-to-exit behavior. Linux closes and exits normally.

macOS uses native traffic lights by default and supports Finder clipboard file URLs, Command+C/V, Command+Option+V for moving, and Command+Delete for crFiles Trash. Its private Trash remains separate from Finder's Trash.

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

On macOS, application shortcuts generally use Command instead of Ctrl; tab cycling remains Control+Tab.

Numeric-keypad plus and minus are also supported with Ctrl. Icon-size shortcuts do not act while a text field has focus.

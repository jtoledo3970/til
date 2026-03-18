---
title: Disabling Windows Python App Execution Aliases
date: 2026-03-17
tags:
  - windows
  - python
  - sysadmin
---

I've been on a Linux heavy workflow for years now and was surprised to find Windows 11 includes "App Execution Aliases" that hijack the `python` and `python3` commands, often redirecting to the Microsoft Store or throwing "Permission Denied" errors even if a valid interpreter is installed via official installers or pyenv-win.

## The Problem
Windows prioritizes its own stubs located in `%USERPROFILE%\AppData\Local\Microsoft\WindowsApps`. These zero-byte files intercept the command before it reaches your actual PATH entries.

## Resolution
You can disable these through the GUI to let your manual installation take priority.

1. Open **Settings** > **Apps** > **Advanced app settings**.
2. Select **App execution aliases**.
3. Toggle **App Installer (python.exe)** and **App Installer (python3.exe)** to **Off**.

Verify the change in PowerShell:
`where.exe python`

The result should now point to your intended installation path (e.g., Program Files or pyenv) rather than the WindowsApps folder.

## Note
Windows Updates occasionally reset these toggles to "On." If your environment suddenly breaks after a system update, check these aliases first.

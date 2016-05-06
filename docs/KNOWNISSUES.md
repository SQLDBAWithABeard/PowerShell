# Known Issues

## `ControlPanelItemCommand.cs`

The file `monad/src/commands/management/ControlPanelItemCommand.cs` has been removed
temporarily from `Microsoft.PowerShell.Commands.Management` because we
cannot resolve `[Shell32.ShellFolderItem]` for FullCLR builds. This must be
fixed ASAP.

## `Microsoft.Management.Infrastructure.Native`

Windows builds currently use the native stub; this should be replaced with
actual compilation of the managed C++ library on Windows (with the stub used on
Linux).

## CorePS Eventing Library

The Eventing library reimplementation for Core PowerShell does not exist on
Linux, and so the ETW stub is used via a `#if LINUX` guard. On Windows, this
library now exists, but its build needs to be ported to .NET CLI. Until then,
the stub is also used with a `#if ETW` guard.

## xUnit

The xUnit tests can only be run on Linux.

## Console Output

Performance issues have been seen in some scenarios, such as nested SSH
sessions. We believe this is likely an issue with `Console.ReadKey()` and are
investigating.

## Remoting

Only basic authentication is implemented

Multiple sessions are not yet supported

Server shut-down is not complete (must restart `omiserver` after a session is
completed.

## Unavailable cmdlets

This project includes the CoreCLR versions of the `Commands.Management`,
`Commands.Utility`, `Security`, and `PSDiagnostics` modules.

The `Archive`, `Diagnostics`, `PSGet`, and `Host` modules are not yet included.

The `WSMan.Management` module cannot be included unless the
`Management.Infrastructure.Native` library is ported.

The CoreCLR version of the `Commands.Utility` module does not contain the
following cmdlets that exist in the FullCLR version:

- ConvertFrom-String
- ConvertTo-Html
- Export-PSSession
- Get-TraceSource
- Import-PSSession
- Invoke-RestMethod
- Invoke-WebRequest
- Out-GridView
- Out-Printer
- Send-MailMessage
- Set-TraceSource
- Show-Command
- Trace-Command
- Update-List
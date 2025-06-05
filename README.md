```mermaid
flowchart TD
    A[Start: windows_post_provision]

    A --> B[Connect via WinRM - Admin]
    B --> C[Copy postcheck.ps1]
    B --> D[Copy ConfigureServer.ps1]

    D --> E[Add Users to Admin Group]
    E --> F[Create ConfigureServerTask]
    F --> G[Run ConfigureServerTask]
    G --> H[Sleep 180 seconds]
    H --> I[Delete ConfigureServerTask]

    I --> J[Check and Run ccmsetup.exe]
    J --> K[Run postcheck.ps1]

    K --> L[Delete ConfigureServer.ps1]
    L --> M[Enable WMI Firewall Rule]
    M --> N[Uninstall RSAT AD PowerShell]

    N --> O[End]

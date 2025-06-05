```mermaid
graph TD
    A[Start: Windows Post-Provisioning] --> B{Establish WinRM Connection<br>(as Administrator)};
    B --> C[Transfer postcheck.ps1];
    C --> D[Transfer ConfigureServer.ps1];
    D --> E[Add Users to Local Admins Group];
    E --> F[Create Scheduled Task 'ConfigureServerTask'];
    F --> G[Wait 20 seconds];
    G --> H[Run ConfigureServerTask];
    H --> I[Wait 180 seconds];
    I --> J[Delete ConfigureServerTask];
    J --> K{Establish New WinRM Connection<br>(as Administrator)};
    K --> L[List C:\Temp\Client contents];
    L --> M{Is ccmsetup.exe present?};
    M -- Yes --> N[Start ccmsetup.exe /quiet /wait];
    M -- No --> O[Write Error: ccmsetup.exe not found];
    N --> P{Establish New WinRM Connection<br>(as BELGIANRAIL\sysp_iac_vmware)};
    O --> P;
    P --> Q[Execute postcheck.ps1];
    Q --> R[Delete ConfigureServer.ps1];
    R --> S[Enable WMI-WINMGMT-In-TCP Firewall Rule];
    S --> T[Uninstall RSAT-AD-PowerShell];
    T --> U[End: Post-Provisioning Complete];

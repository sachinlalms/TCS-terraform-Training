```mermaid
flowchart TD
    A[Start: Apply null_resource.windows_post_provision_sysp] --> B[Connect via WinRM to Windows Host]
    
    B --> C[Upload license.ps1 via file provisioner]
    C --> D[Create scheduled task: LicenseTask]
    D --> E[Run scheduled task: LicenseTask]
    E --> F[Wait for 180 seconds using Start-Sleep]
    F --> G[Delete scheduled task: LicenseTask]

    subgraph Connection_Details
        H1[User: var.license_user]
        H2[Host: var.license_host]
        H3[Port: 5985]
        H4[Protocol: WinRM - insecure, NTLM, HTTP]
        H5[Timeout: 10 minutes]
    end

    B --> H1
    B --> H2
    B --> H3
    B --> H4
    B --> H5

```mermaid
flowchart TD
    A[Terraform applies null_resource.windows_cleanup] --> B[Connect via WinRM to Windows host]
    B --> C[Execute: del C:\\Temp\\postcheck.ps1]
    C --> D[Remove user from Administrators group]
    D --> E[Wait for 60 seconds]
    E --> F[Restart Windows machine]

    subgraph Connection Info
        B1[User: BELGIANRAIL\\sysp_iac_vmware]
        B2[Port: 5985]
        B3[Timeout: 30m]
        B4[Use NTLM: true]
    end

    B --> B1
    B --> B2
    B --> B3
    B --> B4

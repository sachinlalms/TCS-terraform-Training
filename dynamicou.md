```mermaid
flowchart TD
    A[Start get_ou Function] --> B[Connect to AD via LDAP/NTLM]
    B --> C{Datacenter?}
    C --> D1[Muizen]
    C --> D2[Zaventem]
    C --> D3[Other ➜ Error]

    D1 --> E1[Map environment ➜ env_code]
    E1 --> F1{env_code valid?}
    F1 -->|No| Z1[Return Error]
    F1 -->|Yes| G1[Search OU in 'OU=Servers,OU=Resources,OU=env_code']

    G1 --> H1{App Type / Name Matching Rules}
    H1 --> I1[app-sap ➜ SAP - APP / ASCS]
    H1 --> I2[db-sql ➜ SQL]
    H1 --> I3[EIM ➜ EIM - ASCS or APP]
    H1 --> I4[non-sap ➜ Match name or fallback to APP]
    H1 --> I5[Default ➜ APP]

    I1 --> J1[Set selected_ou]
    I2 --> J1
    I3 --> J1
    I4 --> J1
    I5 --> J1

    D2 --> E2[Map environment ➜ env_code]
    E2 --> F2{env_code valid?}
    F2 -->|No| Z1
    F2 -->|Yes| G2[Search OU in 'OU=Servers,OU=TCS']
    G2 --> J2[Match entry.ou == env_code ➜ selected_ou]

    J1 --> K[Return selected_ou]
    J2 --> K
    Z1 --> K

    D3 --> Z2[Return unsupported datacenter error]
    Z2 --> K

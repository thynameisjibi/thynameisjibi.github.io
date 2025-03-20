# Getting Started

## Required Technologies

- Windows Subsystem Linux (WSL) - skip if mac
    - How to install: <https://learn.microsoft.com/en-us/windows/wsl/install>
- Docker
    - How to install (windows): <https://docs.docker.com/desktop/setup/install/windows-install/>
    - How to install (mac): <https://docs.docker.com/desktop/setup/install/mac-install/>
- Node Version Manager (NVM)
    - How to install: <https://github.com/nvm-sh/nvm?tab=readme-ov-file#install--update-script>
- Git
    - How to install (ubuntu): ```sudo apt install git```
    - How to install (mac): ```brew install git```

## Repositories

- REA
    - <https://bitbucket.org/go-va_dev/rea-beta-backend/src/master/>
    - <https://bitbucket.org/go-va_dev/rea-beta-frontend/src/master/>
- REA Automation Backend
    - <https://bitbucket.org/go-va_dev/rea-n8n/src/master/>
- REA Automation Frontend
    - <https://bitbucket.org/go-va_dev/rea-automation-fe/src/master/>

## Application Relationship State Diagram

```mermaid
stateDiagram-v2
    [*] --> REA: User Access
    
    state "REA (Main Application)" as REA {
        [*] --> Authentication
        Authentication --> MainInterface: User Authenticated
        MainInterface --> DisplayingAutomation: Load Automation Interface
    }
    
    state "Multiplai App" as Auth {
        [*] --> LoginProcess
        LoginProcess --> AuthenticationComplete
    }
    
    state "REA Automation Frontend" as Frontend {
        [*] --> InterfaceLoaded
        InterfaceLoaded --> ProcessingUserAction
        ProcessingUserAction --> DisplayingResults
        DisplayingResults --> InterfaceLoaded
    }
    
    state "REA Automation Backend" as N8N {
        [*] --> ReceivingRequest
        ReceivingRequest --> ProcessingRequest
        ProcessingRequest --> DeliveringResponse
    }
    
    REA --> Auth: Authentication Request
    Auth --> REA: Authentication Response
    
    REA --> Frontend: Embed as iframe
    
    Frontend --> N8N: API Calls
    N8N --> Frontend: API Responses
```

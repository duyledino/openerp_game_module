erDiagram

    %% =========================
    %% CORE ENTITY
    %% =========================

    GAME {
        Integer id PK
        String name
        Text description
        Datetime release_date
        Float price
        String status
        Integer publisher_id FK
        Integer studio_id FK
        Integer series_id FK
    }

    %% =========================
    %% GAME VERSION
    %% =========================

    GAME_VERSION {
        Integer id PK
        String version_name
        Text enhancement_notes
        Datetime release_date
        String status
        Integer game_id FK
    }

    GAME ||--o{ GAME_VERSION : "has versions"

    %% =========================
    %% SERIES
    %% =========================

    SERIES {
        Integer id PK
        String name
        Text description
    }

    SERIES ||--o{ GAME : "contains"

    %% =========================
    %% PUBLISHER
    %% =========================

    PUBLISHER {
        Integer id PK
        String name
        String country
    }

    PUBLISHER ||--o{ GAME : "publishes"

    %% =========================
    %% STUDIO
    %% =========================

    STUDIO {
        Integer id PK
        String name
        String headquarter
    }

    STUDIO ||--o{ GAME : "develops"

    %% =========================
    %% MEMBER
    %% =========================

    MEMBER {
        Integer id PK
        String name
    }

    %% Many-to-Many
    STUDIO }o--o{ MEMBER : "has members"

    %% =========================
    %% ROLE
    %% =========================

    ROLE {
        Integer id PK
        String name
    }

    MEMBER }o--o{ ROLE : "has roles"

    %% =========================
    %% GENRE
    %% =========================

    GENRE {
        Integer id PK
        String name
    }

    GAME }o--o{ GENRE : "categorized as"

    %% =========================
    %% PLATFORM
    %% =========================

    PLATFORM {
        Integer id PK
        String name
    }

    GAME }o--o{ PLATFORM : "available on"

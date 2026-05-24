# Video Recording Script

This is a speaking outline, not a full transcript.  
Use it as the order for what to say while recording the module.

## 1. Opening

### What I will say
- Introduce the module as a `game management` addon for OpenERP.
- Say that the module manages game data, publishing info, studios, staff, genres, platforms, series, and game versions.
- Explain that I will first show the design, then the Python models, then the XML views and menus.

## 2. Architecture Overview

### What I will say
- Explain the main entities in the system and how they connect.
- Mention `game` as the core object.
- Mention related objects: `game.version`, `game.series`, `game.publisher`, `game.studio`, `game.member`, `game.role`, `game.genre`, and `game.platform`.
- Say that the architecture shows both one-to-many and many-to-many relationships.

### What I will focus on
- `game` as the central model.
- `game.version` as version history for each game.
- `series`, `publisher`, and `studio` as supporting business entities.
- `member` and `role` as the internal team structure.
- `genre` and `platform` as classification and availability data.

## 3. `game.py` Walkthrough

### 3.1 Game Model

### What I will say
- Introduce `Game` as the main model.
- Explain that it stores the game name, description, release date, price, status, publisher, studio, series, genres, platforms, and versions.
- Mention that this model also includes computed display fields and update status.

### What I will focus on
- Validation in `create` and `write`.
- Name trimming and duplicate checking.
- Price and release date rules.
- The update-check logic for versions.
- The `action_update_game` method.

### 3.2 Publisher Model

### What I will say
- Explain that `Publisher` stores publisher name and country.
- Mention that the model prevents empty names and duplicate publishers.

### 3.3 Studio Model

### What I will say
- Explain that `Studio` represents the development company.
- Mention the studio name, headquarters, and related members.
- Say that it also validates the name before saving.

### 3.4 Member Model

### What I will say
- Introduce `Member` as the staff or employee model.
- Explain that a member can belong to studios and has roles.
- Mention the computed studio display field.

### 3.5 Genre Model

### What I will say
- Explain that `Genre` is a simple reference model for game categories.
- Mention the duplicate and empty-name checks.

### 3.6 Platform Model

### What I will say
- Explain that `Platform` stores the gaming platform name.
- Mention that it works as another reference table for games.

### 3.7 Series Model

### What I will say
- Explain that `Series` groups games into a franchise or collection.
- Mention the optional description field and validation rules.

### 3.8 Role Model

### What I will say
- Explain that `Role` stores employee roles.
- Mention that it is used together with members in the studio structure.

### 3.9 GameVersion Model

### What I will say
- Explain that `GameVersion` stores version name, update notes, and the related game.
- Mention that version names must follow a numeric format.
- Mention the uniqueness check per game.

## 4. `game_view.xml` Walkthrough

### What I will say
- Explain that this file defines the user interface for all models.
- Say that it contains tree views, form views, and window actions.
- Mention that each model gets its own interface for listing and editing records.

### What I will focus on
- The `game` tree view for fast overview.
- The `game` form view for detailed editing.
- The publisher, studio, member, genre, platform, series, role, and version views.
- The action buttons and tabbed layout.

### 4.1 Game Views

### What I will say
- Describe the game list view as the main management screen.
- Mention that it shows important summary fields and update status.
- Explain that the form view is organized into grouped sections and notebooks.

### 4.2 Publisher and Studio Views

### What I will say
- Explain that these views are simple master-data screens.
- Mention that the studio form includes a members tab.

### 4.3 Member, Genre, Platform, Series, Role, and Version Views

### What I will say
- Explain that each supporting model has a tree view and a form view.
- Mention that the version form includes field behavior based on related data.
- Say that these screens keep the module consistent and easy to manage.

## 5. `game_menu.xml` Walkthrough

### What I will say
- Explain that the menu file connects the module to the OpenERP navigation.
- Mention the main menu root for `Quản lý Game`.
- Say that the menu is split into two logical groups.

### What I will focus on
- `Games` group: game, version, series, genre, platform.
- `Tổ chức & Nhân sự` group: publisher, studio, member, role.
- How each menu item opens the correct action from `game_view.xml`.

## 6. Closing Summary

### What I will say
- Summarize that the module combines data modeling, validation, UI, and navigation.
- Mention that `game.py` handles the business logic, `game_view.xml` handles the interface, and `game_menu.xml` handles access from the menu.
- End by saying the module is ready for managing game-related records in one place.


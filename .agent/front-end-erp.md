# Front‑End Development Guide for OpenERP 7 (Game Management Module)

> **Target audience:** 4th‑year student with no prior XML UI experience.

---

## 1️⃣ What is OpenERP 7?
OpenERP 7 (now called Odoo 7) is a **server‑side** framework written in Python. The *front‑end* you see in the browser is generated from **XML view definitions**. The main building blocks are:

| Block | Purpose |
|-------|---------|
| **Model** (`game.game`, `game.publisher`…) | Python class that defines the data (fields, methods). |
| **View** (`ir.ui.view`) | XML description of how the model is displayed – *search*, *tree*, *form*, *graph*, etc. |
| **Action** (`ir.actions.act_window`) | Binds a view (or multiple views) to a model. |
| **Menu** (`ir.ui.menu`) | Navigation entry that triggers an action. |

All four are linked together through the `id` attributes you see in the XML files.

---

## 2️⃣ Core XML Tags (the “vocabulary”)
| Tag | Where it is used | Typical attributes |
|-----|----------------|-------------------|
| `<field>` | Inside `<form>`, `<tree>`, `<search>` | `name`, `string`, `readonly`, `required`, `colspan`, `widget`, `help`, `attrs` |
| `<form>` | Record form (detail view) | `string`, `version` |
| `<tree>` | List view (grid) | `string`, `editable` |
| `<search>` | Search side‑panel | `string` |
| `<group>` | Groups fields in a form | `col`, `string` |
| `<sheet>` | Container for the whole form body (mandatory in v7) | |
| `<notebook>` / `<page>` | Tabbed sections inside a form | |
| `<menuitem>` | Declares a menu entry (see `game_menu.xml`) | `id`, `name`, `parent`, `action`, `sequence`, `icon` |
| `<record>` | Creates a record of a particular model (`ir.ui.view`, `ir.actions.act_window`, `ir.ui.menu`) | |

> **Tip:** All tags are inside `<openerp><data>...</data></openerp>`.

---

## 3️⃣ Full Example: `game_view.xml` (with enhancements)
```xml
<?xml version="1.0" encoding="utf-8"?>
<openerp>
    <data>
        <!-- SEARCH VIEW -->
        <record model="ir.ui.view" id="view_game_search">
            <field name="name">game.search</field>
            <field name="model">game.game</field>
            <field name="type">search</field>
            <field name="arch" type="xml">
                <search string="Tìm kiếm game">
                    <field name="name" string="Tên game"/>
                    <field name="genre" string="Thể loại"/>
                    <field name="publisher_id" string="Nhà phát hành"/>
                    <field name="status" string="Trạng thái"/>
                    <field name="studio_id" string="Nhà phát triển"/>
                    <!-- Quick filters -->
                    <filter name="released_games" string="Đã phát hành"
                            domain="[('status', '=', 'released')]"/>
                    <filter name="upcoming_games" string="Sắp phát hành"
                            domain="[('status', '=', 'upcoming')]"/>
                    <!-- Price range filters (new) -->
                    <filter name="price_low" string="Giá < 100k"
                            domain="[('price','<',100000)]"/>
                    <filter name="price_high" string="Giá > 1M"
                            domain="[('price','>',1000000)]"/>
                </search>
            </field>
        </record>

        <!-- TREE VIEW (inline editing enabled) -->
        <record model="ir.ui.view" id="view_game_tree">
            <field name="name">game.tree</field>
            <field name="model">game.game</field>
            <field name="type">tree</field>
            <field name="arch" type="xml">
                <tree string="Danh sách các tựa game" editable="bottom">
                    <field name="name"/>
                    <field name="genre"/>
                    <field name="studio_id"/>
                    <field name="publisher_id"/>
                    <field name="status"/>
                    <field name="price"/>
                </tree>
            </field>
        </record>

        <!-- FORM VIEW (tooltips, conditional attrs, many2many widget) -->
        <record model="ir.ui.view" id="view_game_form">
            <field name="name">game.form</field>
            <field name="model">game.game</field>
            <field name="type">form</field>
            <field name="arch" type="xml">
                <form string="Thông tin Game" version="7.0">
                    <header/>
                    <sheet>
                        <!-- Main title spans 4 columns -->
                        <group col="4">
                            <field name="name" colspan="4" string="Tên game:"/>
                        </group>
                        <!-- Basic info -->
                        <group col="2" string="Thông tin cơ bản">
                            <field name="genre" string="Thể loại:"/>
                            <field name="status" string="Trạng thái:"/>
                            <field name="release_date" string="Ngày phát hành:" attrs="{'readonly':[('status','=','released')]}"/>
                            <field name="price" string="Giá:" help="Giá bán cuối cùng (đơn vị VND)"/>
                        </group>
                        <!-- Publishing info -->
                        <group col="2" string="Thông tin phát hành">
                            <field name="publisher_id" string="Nhà phát hành:"/>
                            <field name="studio_id" string="Nhà phát triển:"/>
                            <field name="series_id" string="Series:"/>
                        </group>
                        <!-- Platforms (many2many tags) -->
                        <group col="4">
                            <field name="platform_ids" widget="many2many_tags" string="Nền tảng:" colspan="4"/>
                        </group>
                        <!-- Notebook with description and notes -->
                        <notebook>
                            <page string="Mô tả">
                                <field name="description" nolabel="1"/>
                            </page>
                            <page string="Chi tiết">
                                <field name="notes" nolabel="1" placeholder="Thêm các chi tiết bổ sung về tựa game..."/>
                            </page>
                        </notebook>
                    </sheet>
                </form>
            </field>
        </record>

        <!-- ACTION (binds the three views) -->
        <record model="ir.actions.act_window" id="action_game">
            <field name="name">Thông tin Game</field>
            <field name="res_model">game.game</field>
            <field name="view_type">form</field>
            <field name="view_mode">tree,form</field>
        </record>
    </data>
</openerp>
```

### What changed compared to the original file?
* Added **price range filters** in the search view.
* Enabled **inline editing** on the tree view (`editable="bottom"`).
* Added **help tooltips** (`help="…"`) on the `price` field.
* Made `release_date` **read‑only** when status is `released` using `attrs`.
* Rendered the many‑to‑many relationship `platform_ids` with the `many2many_tags` widget.
* Re‑ordered fields for a more logical user flow.

---

## 4️⃣ Full Example: `game_menu.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>
<openerp>
    <data>
        <!-- Root menu for the whole addon -->
        <menuitem id="game_parent" name="Quản lý Game" icon="STOCK_OPEN"/>

        <!-- Games submenu (games, series, genres, platforms) -->
        <menuitem id="menu_game_parent" name="Games" parent="game_parent" sequence="10"/>
        <menuitem id="menu_game_list" name="Danh sách game" parent="menu_game_parent" action="action_game" sequence="10"/>
        <menuitem id="menu_series_list" name="Series" parent="menu_game_parent" action="action_series" sequence="20"/>
        <menuitem id="menu_genre_list" name="Thể loại" parent="menu_game_parent" action="action_genre" sequence="30"/>
        <menuitem id="menu_platform_list" name="Nền tảng" parent="menu_game_parent" action="action_platform" sequence="40"/>

        <!-- Company & HR submenu -->
        <menuitem id="menu_company_parent" name="Tổ chức &amp; Nhân sự" parent="game_parent" sequence="20"/>
        <menuitem id="menu_publisher_list" name="Nhà phát hành" parent="menu_company_parent" action="action_publisher" sequence="10"/>
        <menuitem id="menu_studio_list" name="Nhà phát triển" parent="menu_company_parent" action="action_studio" sequence="20"/>
        <menuitem id="menu_member_list" name="Nhân viên" parent="menu_company_parent" action="action_member" sequence="30"/>
    </data>
</openerp>
```

### How the menu works
* `game_parent` is the top‑level entry that appears in the left navigation.
* Child menus (`menu_game_parent`, `menu_company_parent`) are grouped under it.
* Each leaf (`menu_game_list`, `menu_publisher_list`, …) points to an **action** defined elsewhere (`action_game`, `action_publisher`, …). When the user clicks the leaf, OpenERP opens the corresponding view.

---

## 5️⃣ How to Test Your Changes
1. **Save the two XML files** (`game_view.xml` and `game_menu.xml`) with the content above.
2. Restart the server or run the update command you already use:
   ```bash
   .\\openerp-server.exe -c .\\openerp-server.conf -d duy_cor -u game_management
   ```
3. Open the web UI, go to **Quản lý Game → Games → Danh sách game**.
4. Verify the following:
   * New price‑range filters appear on the left panel.
   * Hovering over the *Giá* field shows the tooltip.
   * The *release_date* field becomes read‑only after you set *Trạng thái* to `released`.
   * Inline editing works directly in the list view.
   * The *Nền tảng* field shows selectable tags.
5. Navigate to the other menu entries (Series, Thể loại, Nhà phát hành, …) to make sure the menu hierarchy works.

---

## 6️⃣ Recap
* OpenERP 7 UI is **declarative XML** – you describe *what* to show, not *how* to render it.
* The **view hierarchy** you’ll use most often is **search → tree → form**.
* Common patterns to master:
  * **Tooltips** (`help`), **conditional attributes** (`attrs`), **widgets** (`many2many_tags`).
  * **Inline editing** (`editable="bottom"` on `<tree>`).
  * **Filters** (`<filter>` in `<search>`).
* The **menu file** simply wires actions to a navigation tree.

Happy coding! If any XML syntax error appears, copy the error message and ask for a quick fix – we’ll correct it together.

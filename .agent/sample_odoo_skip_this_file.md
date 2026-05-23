views.xml
<?xml version="1.0" encoding="UTF-8"?>
<odoo>
    <!-- List View (Replaces Tree View in Odoo 18) -->
    <record id="student_student_view_tree" model="ir.ui.view">
        <field name="name">student.student.tree.view</field>
        <field name="model">student.student</field>
        <field name="arch" type="xml">
            <list>
                <field name="name"/>
                <field name="student_id"/>
                <field name="dob"/>
                <field name="gender"/>
            </list>
        </field>
    </record>

    <!-- Form View -->
    <record id="student_student_view_form" model="ir.ui.view">
        <field name="name">student.student.form.view</field>
        <field name="model">student.student</field>
        <field name="arch" type="xml">
            <form>
                <group>
                    <field name="name"/>
                    <field name="student_id"/>
                    <field name="image"/>
                    <field name="dob"/>
                    <field name="gender"/>
                    <field name="email"/>
                    <field name="phone"/>
                    <field name="address"/>
                    <field name="guardian_name"/>
                    <field name="guardian_phone"/>
                    <field name="admission_date"/>
                </group>
            </form>
        </field>
    </record>
</odoo>


view_memu.xml

<?xml version="1.0" encoding="UTF-8"?>
<odoo>
    <!-- Action View -->
    <record id="student_student_action" model="ir.actions.act_window">
        <field name="name">Student</field>
        <field name="res_model">student.student</field>
        <field name="view_mode">list,form</field>
    </record>

    <!-- Root Menu -->
    <menuitem id="student_student_root_menu" name="Student Management" sequence="0"/>

    <!-- Sub Menu -->
    <menuitem id="student_student_menu" name="Students" parent="student_student_root_menu" action="student_student_action" sequence="0"/>
</odoo

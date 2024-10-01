# Database-Creation-Deletion
//Full detailed explanation of the file shared

alter session set container=cdb$root;
This command switches the context to the root container (cdb$root), which is necessary for managing PDBs.

show pdbs;
This command lists all pluggable databases in the CDB, showing the CON_ID, CON_NAME, OPEN MODE, and RESTRICTED mode.

alter pluggable database de_to_delete_pdb close immediate;
This closes the de_to_delete_pdb database immediately, meaning no new connections are allowed, and existing ones are terminated.

alter pluggable database de_to_delete_pdb unplug into 'D:\oracle19c\admin\orcl\pdump\de_to_delete_pdb.xml';
The unplug command removes the PDB from the CDB but creates an XML metadata file (de_to_delete_pdb.xml) to preserve its structure.

drop pluggable database de_to_delete_pdb;
This command permanently removes the de_to_delete_pdb after unplugging.

create pluggable database plsql_class2024 admin user pdbadmin identified by 1234 file_name_convert= ...
This creates a new pluggable database called plsql_class2024 with an administrative user (pdbadmin), identified by the password 1234.
The file_name_convert option maps the data files for the new PDB based on the template from pdb$seed.

alter pluggable database plsql_class2024 open;
After creating the PDB, this command opens the plsql_class2024 PDB, making it available for connections.

alter pluggable database plsql_class2024 save state;
The save state command ensures that the PDB will automatically open whenever the CDB is restarted.

create user de_plsqlaunca identified by 1234;
grant all privileges to de_plsqlaunca;
A new user, de_plsqlaunca, is created with the password 1234 and is granted all privileges within the plsql_class2024 PDB.

create pluggable database de_to_delete_pdb from orclpdb file_name_convert= ...;
A new PDB (de_to_delete_pdb) is created from an existing orclpdb.

alter pluggable database de_to_delete_pdb open;
alter pluggable database de_to_delete_pdb save state;
These commands open the newly created de_to_delete_pdb PDB and save its state for automatic opening after restarts.

alter pluggable database de_to_delete_pdb close immediate;
alter pluggable database de_to_delete_pdb unplug into 'D:\oracle19c\admin\orcl\pdump\de_to_delete_pdb.xml';
drop pluggable database de_to_delete_pdb;
This repeats the process of closing, unplugging, and dropping the de_to_delete_pdb as seen in the first image.

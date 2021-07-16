Introduction
=============
This project will demonstrate, persistence.

Versions
========
EAP: JBOSS 7.3.3
RHPAM: 7.10.1

Create a new Datasource
(needed if the persistable variable need to be persisted in different schema)
Refer to the official documentation to create a new Datasource  https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.3/html/configuration_guide/datasource_management
example(mysql):

<xa-datasource jndi-name="java:jboss/datasources/TEMENOS_SCHEMA" pool-name="TEMENOS_SCHEMA" enabled="true" use-java-context="true" use-ccm="true">
  <xa-datasource-property name="ServerName">localhost</xa-datasource-property>
  <xa-datasource-property name="DatabaseName">TEMENOS_SCHEMA</xa-datasource-property>
  <driver>mysql</driver>
  <security>
    <user-name>TEMENOS_USER</user-name>
    <password>PA$$W)RD</password>
  </security>
  <validation>
    <valid-connection-checker class-name="org.jboss.jca.adapters.jdbc.extensions.mysql.MySQLValidConnectionChecker"/>
    <validate-on-match>true</validate-on-match>
    <background-validation>false</background-validation>
    <exception-sorter class-name="org.jboss.jca.adapters.jdbc.extensions.mysql.MySQLExceptionSorter"/>
  </validation>
</xa-datasource>

Create and configure a persistable variable
===========================================
1.Create a new Data Object and flag "Persistable"
2.Create the needed field. Example:
3.Navigate to Settings > Persistence
4.Insert the jndi name of the datasource
5.Set the correct hibernate.dialect
6.In the "Project Persistable Data Objects" add the fully qualified name of the created Data Object


Use the variable in a process
=============================
1.Create a new process definition
2.Create a new process variable
3.Add an output variable to the Human Task
4.Save, Build and deploy

Test the process
=================
1.Create a new instance of the process
2.Claim, start and complete the human task
3.Verify the variable instance has been saved on the external database
4.Verify in PAM 7 database that in the table VariableInstanceLog the inserted data are not visible

Point of attention (NOTE)
=========================



Official documentation:
=======================
PAM 7.9 persist variable: https://access.redhat.com/documentation/en-us/red_hat_process_automation_manager/7.9/html-single/managing_red_hat_process_automation_manager_and_kie_server_settings/index#process-variables-persist-proc_execution-server
JBoss EAP 7.3 datasource: https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.3/html/configuration_guide/datasource_management
External resources: https://karinavarela.me/2020/06/17/persisting-custom-data-configuring-external-persistence/

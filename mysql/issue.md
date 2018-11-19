
1.[Err] 1055 - Expression #1 of ORDER BY clause is not in GROUP BY clause and contains nonaggregated column 'information_schema.PROFILING.SEQ' which is not functionally dependent on columns in GROUP BY clause; this is incompatible with sql_mode=only_full_group_by

<p>Server SQL Modes</p>

The MySQL server can operate in different SQL modes, and can apply these modes differently for different clients, depending on the value of the sql_mode system variable. DBAs can set the global SQL mode to match site server operating requirements, and each application can set its session SQL mode to its own requirements.



deal:
  https://dev.mysql.com/doc/refman/5.7/en/sql-mode.html
  
  
  Setting the SQL Mode

The default SQL mode in MySQL 5.7 includes these modes: ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, and NO_ENGINE_SUBSTITUTION.

These modes were added to the default SQL mode in MySQL 5.7: The ONLY_FULL_GROUP_BY and STRICT_TRANS_TABLES modes were added in MySQL 5.7.5. The NO_AUTO_CREATE_USER mode was added in MySQL 5.7.7. The ERROR_FOR_DIVISION_BY_ZERO, NO_ZERO_DATE, and NO_ZERO_IN_DATE modes were added in MySQL 5.7.8. For additional discussion regarding these changes to the default SQL mode value, see SQL Mode Changes in MySQL 5.7.

To set the SQL mode at server startup, use the --sql-mode="modes" option on the command line, or sql-mode="modes" in an option file such as my.cnf (Unix operating systems) or my.ini (Windows). modes is a list of different modes separated by commas. To clear the SQL mode explicitly, <p1>set it to an empty string using --sql-mode="" on the command line, or sql-mode="" in an option file.</p1>

Note
